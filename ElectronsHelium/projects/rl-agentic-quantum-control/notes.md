# Notes — RL and agentic optimization for gates and sensing

Informal brainstorm space. Move stable material into `main.tex`; keep this as the scratch pad.

## Core question
Can the PPO-based trap optimization already used for sensing (`perruzza2026`) be ported to gate
design (currently grid search in `leinonen2025`), and is a joint gate+sensing reward, or a
higher-level "agentic" layer on top, actually useful — or just more complicated for no real gain?

## Connections to existing skills/papers
- `ci-dvr-hartree-numerics` — the RL/PPO scaffolding already exists here (see its "Optimize" step);
  this project's environment should be built as an extension of that, not a parallel one.
- `two-qubit-gates` — current grid-search optimization to compare against; same fidelity metrics
  (swap error, leakage error, gate time, robustness to ramp/hold deviations) should be reused.
- `quantum-sensing` — existing PPO reward (`r_f · r_cfi − penalties`) and hyperparameters (paper's
  Table 1) to reuse/extend for the joint reward.

## Open physics/engineering questions
- Is there evidence the erf-ramp family in `leinonen2025` is actually suboptimal, or does grid
  search already find near-optimal solutions for this specific Hamiltonian? Worth a quick sanity
  check (e.g. compare RL-found pulse against erf ramp on a toy version of the problem) before
  committing to a full RL implementation.
- Sample efficiency: gate simulations (Crank–Nicolson propagation) are presumably more expensive
  per-episode than the sensing reward evaluation — check wall-clock budget before designing the
  training loop.
- What's a concrete use case for the joint gate+sensing reward? Don't build it just because it's
  possible.
- Define "agentic" precisely before using the word in the manuscript — right now it's a placeholder
  for "something more than parameter optimization" and needs to become a specific, testable claim.
- Model-aware RL, add material about it
## Equations / derivations to work out
- Action-space parametrization for the gate-RL environment (direct voltage increments vs. a
  truncated smooth-basis expansion of λ(t)).
- Multi-objective reward weighting scheme, if the joint reward is pursued.

## Numerics needed
- Python first (reuse `src/eoh/rl.py` scaffold from `src/README.md`); C++/Fortran (OO) only if
  Crank–Nicolson propagation inside the RL loop becomes the bottleneck. Present training curves and
  discovered pulse shapes in a notebook, e.g. `notebooks/06_rl_optimization.ipynb` (already listed
  in `notebooks/README.md`) extended with a gate-design section, or a new
  `notebooks/08_rl_gate_design.ipynb`.

## Risks / open challenges
- RL training cost vs. grid search: if grid search is already cheap and good, RL needs a clear
  advantage (robustness? richer pulse families?) to be worth the added complexity — be honest about
  this in the manuscript rather than assuming RL is automatically better.
- Keep claims-discipline: label anything RL "discovers" as such, and don't present a single training
  run's result as a general conclusion without checking seed-to-seed variance.
