# Reinforcement learning and agentic optimization for quantum gates and quantum sensing

**Status:** idea / outline. No results yet — see `main.tex` for the motivating introduction and
outlined RL environment, and `notes.md` for the open-questions scratch pad.

**Pitch:** the eHe platform already uses PPO-based reinforcement learning to optimize the trap for
entanglement-enhanced sensing (`perruzza2026`), but two-qubit gate design (`leinonen2025`) still
uses a small grid search. This project ports RL to gate design, explores a joint gate-and-sensing
reward, and (more speculatively) a higher-level "agentic" optimization/planning layer — though that
last piece needs a much sharper definition before it's a real research claim (see `notes.md`).

**Target journal:** TBD — Phys. Rev. Applied or a Quantum-technology-focused venue are plausible
given the RL-for-quantum-control literature this connects to; `main.tex` class options default to
`prapplied`.

**Related skills:** `ci-dvr-hartree-numerics` (existing RL/PPO scaffolding to extend),
`two-qubit-gates` (grid-search baseline to beat), `quantum-sensing` (existing PPO reward to reuse).

**First concrete task:** a quick sanity check on whether RL actually beats the existing erf-ramp
grid search on a toy version of the gate problem, before committing to a full implementation —
see `notes.md`.
