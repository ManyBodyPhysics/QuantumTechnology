# Code templates

Adapt these; they encode the conventions used across the project (natural units, soft Coulomb,
distinguishable-particle product basis). Python (NumPy/SciPy) is the reference implementation; move
hot loops to C++/Fortran once correctness is pinned down against these.

## Table of contents
- [1. sinc-DVR kinetic matrix](#1-sinc-dvr-kinetic-matrix)
- [2. Soft Coulomb & potential](#2-soft-coulomb--potential)
- [3. Hartree self-consistency](#3-hartree-self-consistency)
- [4. CI assembly & diagonalization](#4-ci-assembly--diagonalization)
- [5. Entanglement entropy (SVD)](#5-entanglement-entropy-svd)
- [6. Crank–Nicolson propagation](#6-crank-nicolson-propagation)
- [7. Fisher information & Cramér–Rao](#7-fisher-information--cramér-rao)
- [8. Pushing kernels to C++/Fortran](#8-pushing-kernels-to-cfortran)
- [9. Notebook / Jupyter-book layout](#9-notebook--jupyter-book-layout)

## 1. sinc-DVR kinetic matrix
```python
import numpy as np

def sinc_dvr_kinetic(n: int, dx: float) -> np.ndarray:
    """1D sinc-DVR kinetic energy matrix in natural units (hbar^2/2m = 1)."""
    i = np.arange(n)
    d = i[:, None] - i[None, :]
    with np.errstate(divide="ignore", invalid="ignore"):
        T = (-1.0) ** d / (dx**2 * d**2)
    np.fill_diagonal(T, np.pi**2 / (6.0 * dx**2))
    return T
```

## 2. Soft Coulomb & potential
```python
KAPPA, EPS = 2326.0, 1e-2  # project conventions

def soft_coulomb(xL: np.ndarray, xR: np.ndarray) -> np.ndarray:
    """Diagonal two-body Coulomb u^{LR}_{gd} on the (left,right) grids."""
    r = xL[:, None] - xR[None, :]
    return KAPPA / np.sqrt(r**2 + EPS**2)

def electrode_potential(x: np.ndarray, alpha: np.ndarray, V: np.ndarray) -> np.ndarray:
    """v(x) = -sum_k alpha_k(x) V_k;  alpha shape (n_electrodes, len(x))."""
    return -(alpha.T @ V)
```

## 3. Hartree self-consistency
```python
def hartree(hL, hR, uLR, tol=1e-10, max_iter=500):
    """Coupled mean-field for two distinguishable particles.
    hL,hR: (n,n) one-body; uLR: (n,n) diagonal two-body couplings."""
    nL, nR = hL.shape[0], hR.shape[0]
    bL = np.linalg.eigh(hL)[1][:, 0].copy()
    bR = np.linalg.eigh(hR)[1][:, 0].copy()
    eL_old = eR_old = np.inf
    for _ in range(max_iter):
        fL = hL + np.diag(uLR @ (bR**2))          # mean field from right density
        fR = hR + np.diag(uLR.T @ (bL**2))        # mean field from left density
        eL, UL = np.linalg.eigh(fL); eR, UR = np.linalg.eigh(fR)
        bL, bR = UL[:, 0], UR[:, 0]
        if abs(eL[0]-eL_old) < tol and abs(eR[0]-eR_old) < tol:
            break
        eL_old, eR_old = eL[0], eR[0]
    return (eL, UL), (eR, UR)                      # keep lowest N_A+1 columns downstream
```

## 4. CI assembly & diagonalization
```python
def ci_hamiltonian(hL, hR, u):
    """H_{ij,kl} = hL_{ik} d_{jl} + d_{ik} hR_{jl} + u_{ij,kl}, flattened to (NL*NR, NL*NR).
    u has shape (NL,NR,NL,NR) in the Hartree product basis."""
    NL, NR = hL.shape[0], hR.shape[0]
    H = (np.einsum("ik,jl->ijkl", hL, np.eye(NR))
         + np.einsum("ik,jl->ijkl", np.eye(NL), hR)
         + u)
    return H.reshape(NL*NR, NL*NR)

def ci_solve(H, k=6):
    from scipy.sparse.linalg import eigsh
    from scipy.sparse import csr_matrix
    E, C = eigsh(csr_matrix(H), k=k, which="SA")   # Davidson-like; lowest k
    return E, C
```

## 5. Entanglement entropy (SVD)
```python
def von_neumann_entropy(C_matrix: np.ndarray) -> float:
    """C_matrix: (NL, NR) coefficient matrix of one eigenstate. Base-2 entropy."""
    s = np.linalg.svd(C_matrix, compute_uv=False)
    p = s**2; p = p[p > 1e-16]
    return float(-np.sum(p * np.log2(p)))
```

## 6. Crank–Nicolson propagation
```python
def crank_nicolson_step(psi, H, dt):
    """Unitary CN step: (1 + i H dt/2) psi_{t+dt} = (1 - i H dt/2) psi_t."""
    n = H.shape[0]; I = np.eye(n)
    A = I + 0.5j * dt * H
    b = (I - 0.5j * dt * H) @ psi
    return np.linalg.solve(A, b)
# dt ~ (omega_qubit/2pi)^{-1}/100 ~ 1e-3 ns for ~10 GHz. Check ||U^dag U - I|| after propagation.
```

## 7. Fisher information & Cramér–Rao
```python
def qfi_pure(psi, dpsi):
    """Quantum Fisher information for a pure state: F_Q = 4(<dpsi|dpsi> - |<psi|dpsi>|^2)."""
    a = np.vdot(dpsi, dpsi).real
    b = abs(np.vdot(psi, dpsi))**2
    return 4.0 * (a - b)

def cfi_binary(P, dP):
    """Classical FI for a binary readout with outcome prob P(phi): (dP)^2 / (P(1-P))."""
    denom = P * (1.0 - P)
    return np.where(denom > 1e-15, dP**2 / denom, 0.0)

# CRB: Var(phi_est) >= 1/(nu * F).  Always assert cfi <= qfi (+ small tol).
# Effective 2-level sensing: P_ge(t) = 4 lam^2/(D^2+4 lam^2) * sin^2( t/2 * sqrt(D^2+4 lam^2) )
#   lam = g muB dB/2 * M_ge,  D = Delta_ST,  natural units hbar=1.
```

## 8. Pushing kernels to C++/Fortran
Keep the Python above as the reference/oracle; port only the bottlenecks (CI matrix–vector products,
propagation solves, RL rollouts). Guidance:
- **C++ (object-oriented):** classes like `DVRGrid`, `HartreeSolver`, `CIHamiltonian`, `Propagator`;
  use Eigen for linear algebra; expose with **pybind11**. Return NumPy-compatible arrays.
- **Fortran (object-oriented, F2008+):** derived types with `type-bound procedures` mirroring the
  same classes; LAPACK for eigensolves; expose via **`iso_c_binding`** (or `f2py` for quick starts).
- **Parity tests are mandatory:** every ported kernel must reproduce the Python result to ~1e-10 on a
  small case before use. Store these as pytest cases in `src/` (see `src/README.md`).
- Parallelize the embarrassingly parallel layers first (voltage/parameter sweeps, RL environments,
  Fisher-information-vs-time scans) before threading the linear algebra.

## 9. Notebook / Jupyter-book layout
Keep logic in importable modules under `src/`; notebooks stay thin (narrative + calls + figures).
Suggested `notebooks/` progression, each a chapter of a Jupyter-book:
1. `01_platform_and_units.ipynb` — units, constants, device geometry, sanity plots.
2. `02_dvr_single_particle.ipynb` — DVR grids, `H_sp`, localized orbitals.
3. `03_hartree_ci_entanglement.ipynb` — Hartree, CI, configurations I/II/III, entropy.
4. `04_two_qubit_gates.ipynb` — `V(λ(t))`, Crank–Nicolson, √iSWAP/CZ fidelity maps.
5. `05_quantum_sensing.ipynb` — `H_B(δB)`, `P_{g→e}`, QFI/CFI, Ramsey benchmark.
6. `06_rl_optimization.ipynb` — PPO reward, trap optimization.
Build with `jupyter-book build .`; pin the environment; seed RNGs; cache expensive diagonalizations.
