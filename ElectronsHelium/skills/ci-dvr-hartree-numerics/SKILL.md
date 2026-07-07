---
name: ci-dvr-hartree-numerics
description: >-
  The shared computational toolkit for the electrons-on-helium project: discrete-variable
  representation (sinc-DVR / DVR) single-particle bases and kinetic matrices, the Hartree method for
  distinguishable particles, full configuration interaction (CI) by exact diagonalization,
  time-dependent propagation (Crank–Nicolson) and Davidson eigensolves, quantum/classical Fisher
  information evaluation, and reinforcement-learning (PPO) optimization of trap potentials. Use this
  skill whenever the user needs to implement, structure, debug, or reason about the numerics behind
  any eHe/DQD calculation — grids and matrix elements, diagonalization, entanglement entropy from a
  coefficient matrix, real-time propagation, Fisher-information/Cramér–Rao computation, or RL reward
  design — or when writing code (Python first; C++/Fortran for heavy kernels) or Jupyter
  notebooks/books for this project. Reach for it even when the physics skills already describe the
  method, because this holds the concrete recipes, code templates, and numerical-hygiene guidance.
---

# Numerical toolkit: DVR · Hartree · CI · propagation · Fisher information · RL

Concrete recipes and code scaffolding shared by `coulomb-entanglement`, `two-qubit-gates`, and
`quantum-sensing`. The physics skills say *what* is computed; this says *how*, with numerical hygiene
and templates. Default language is **Python** (NumPy/SciPy); push hot kernels to **C++ or Fortran**
(object-oriented) and expose them via bindings; present and discuss results in **Jupyter
notebooks / Jupyter-book**.

## What to read when

- **Grids & kinetic/potential/Coulomb matrix elements** → `references/dvr.md`.
- **Hartree self-consistency and full CI assembly/diagonalization** → `references/hartree-ci.md`.
- **Ready-to-adapt code** (Python templates + C++/Fortran kernel notes + notebook layout) →
  `references/code-templates.md`.

## The calculation pipeline (end to end)

1. **Build single-particle bases.** sinc-DVR per well; cut the grid at the barrier `x_b` to confine
   each electron to its own well (effective infinite wall). Kinetic matrix has closed form; potential
   and soft-Coulomb are diagonal on the quadrature. → `references/dvr.md`.
2. **Hartree.** Solve the two coupled mean-field eigenproblems self-consistently
   (`|ε^{(k+1)} − ε^{(k)}| < 1e-10`) to get compact bases `{|φ^A_i⟩}` that pre-absorb the Coulomb
   mean field. → `references/hartree-ci.md`.
3. **CI.** Assemble `H_{ij,kl} = h^L_{ik}δ_{jl} + δ_{ik}h^R_{jl} + u_{ij,kl}` in the Hartree product
   basis; diagonalize for `{E_n, C_{ij,n}}`. For dynamics, get the lowest states with **Davidson**.
4. **Analyze.** Entanglement entropy from the SVD of `C_{ij,n}` (base-2 log); dominant natural
   orbitals from the L/R blocks of the one-body density matrix; overlaps with reference `|S*⟩,|T₀*⟩`.
5. **Encode a signal / propagate.** Add `H_B(δB)` or ramp `V(λ(t))`; propagate the qubit states with
   **Crank–Nicolson** (`Δt ≈ (ω_qubit/2π)⁻¹/100`); build `U_{ij}` overlaps; apply single-qubit `Z`.
6. **Metrology.** Evaluate `F_Q`, `F_C`, `P_{g→e}(t)`; report the Cramér–Rao bound. → `quantum-sensing`.
7. **Optimize.** Grid-search (t_ramp,t_hold) for gates; **PPO** over voltages for sensing reward.

## Units and constants (keep identical across the project)

- Natural units `ℏ²/2mₑ = 1`, `ℏ = 1` (⇒ `mₑ = ½`); time then has units of `µm²`.
- Energy unit `E_d = ℏ²/(mₑ x₀²)`, length unit `x₀ = 123 nm`; soft-Coulomb strength `κ = 2326`,
  regularizer `ε = 1e-2`. Always print at least one conversion to physical units (T, ns, µm).
- Resonator/qubit working range `5–15 GHz`; `N_x = N_y = 20` (400 grid points) is the reference 2D
  grid size; electron separation `d ≈ 1.5 µm`; He depth `h = 500 nm`. See `literature-and-notation`.

## Numerical hygiene (learned from the three papers)

- **Distinguishable-particle product basis** is valid for deep wells (barrier suppresses tunnelling);
  it was validated against antisymmetrized fermionic CI — mention this when someone worries about
  exchange. Use product states, not Slater determinants, for speed.
- **Truncate the CI basis by one-body energy sum** `ε_a + ε_b`, keeping the lowest `N_CI`
  configurations; this avoids dropping low-energy mixed-orbital configs near avoided crossings.
- **Hermiticity & unitarity checks.** Symmetrize Hamiltonian matrices; verify `‖U†U − 1‖` after
  propagation; Crank–Nicolson is unitary by construction — use it (not naive Euler) for gate dynamics.
- **Warm-start** grid searches across hold times (reuse the previous propagation) — large speedups.
- **Fisher-information dips** are physical (readout insensitivity where `∂_ϕ P = 0`), not bugs; keep
  `F_C ≤ F_Q` as a sanity check.
- **Convergence:** check vs grid size `N`, box length `L`, basis truncation `N_CI`, and time step
  `Δt`. Report what was converged.

## Language & delivery preferences for this project

- **Python (NumPy/SciPy)** for orchestration, prototyping, plotting, and the RL loop.
- **C++ or Fortran (object-oriented)** for the heavy kernels (matrix-element assembly, CI
  diagonalization, propagation) when Python is too slow; wrap with pybind11 / `f2py` / `iso_c_binding`
  and keep a pure-Python reference implementation for testing/parity.
- **Jupyter notebooks** for exploration and **Jupyter-book** for the written narrative + reproducible
  figures. Keep each notebook focused (one physics question) and importable-module-backed (logic in
  `src/`, thin notebooks on top). See `notebooks/README.md` and `src/README.md`.

Templates and skeletons: `references/code-templates.md`.
