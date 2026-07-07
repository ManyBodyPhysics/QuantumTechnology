# Notebooks

Jupyter notebooks for exploration and as chapters of a Jupyter-book. Keep notebooks **thin**: put
reusable logic in `../src/` and call it here; notebooks hold narrative, parameter choices, and
figures.

Suggested progression (one physics question per notebook):

1. `01_platform_and_units.ipynb` — units/constants, device geometry, sanity plots.
2. `02_dvr_single_particle.ipynb` — DVR grids, single-particle Hamiltonian, localized orbitals.
3. `03_hartree_ci_entanglement.ipynb` — Hartree, CI, configurations I/II/III, von Neumann entropy.
4. `04_two_qubit_gates.ipynb` — V(λ(t)), Crank–Nicolson propagation, √iSWAP/CZ fidelity maps.
5. `05_quantum_sensing.ipynb` — H_B(δB), P_{g→e}(t), QFI/CFI, Ramsey benchmark.
6. `06_rl_optimization.ipynb` — PPO reward, trap optimization.

Recipes and templates: `../skills/ci-dvr-hartree-numerics/references/code-templates.md`.

## Building a Jupyter-book
```bash
pip install jupyter-book
jupyter-book build .
```
Pin the environment, seed RNGs, and cache expensive diagonalizations so figures are reproducible.
