# src — reference implementation

Python-first library backing the notebooks and any C++/Fortran kernels. Suggested module layout:

```
src/eoh/
├── __init__.py
├── units.py          # natural units, constants (kappa=2326, eps=1e-2, x0=123 nm, ...)
├── dvr.py            # sinc-/sine-DVR grids, kinetic/potential/Coulomb matrix elements
├── hartree.py        # self-consistent Hartree for distinguishable particles
├── ci.py             # CI assembly, Davidson/eigsh, entanglement entropy, natural orbitals
├── dynamics.py       # V(lambda(t)) ramps, Crank–Nicolson propagation, gate fidelity
├── sensing.py        # H_B(dB), P_ge(t), quantum/classical Fisher information, Cramér–Rao
├── rl.py             # PPO environment + reward for trap optimization
└── kernels/          # optional C++/Fortran hot kernels (pybind11 / iso_c_binding), + parity tests
tests/                # pytest: parity of kernels vs Python; convergence checks
```

Keep a pure-Python reference for everything; port only bottlenecks and test them to ~1e-10 on small
cases. Conventions and formulas: `../skills/ci-dvr-hartree-numerics/` and
`../skills/literature-and-notation/references/notation.md`.
