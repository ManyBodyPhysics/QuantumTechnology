# Notes — Two electrons on helium as a Majorana-mode sensor

Informal brainstorm space. Move stable material into `main.tex`; keep this as the scratch pad.

## Core question
Can the singlet differential-sensor scheme from `perruzza2026` (`quantum-sensing` skill) be
repurposed to detect a local signature of a Majorana zero mode (MZM) in a nearby topological
superconductor, exploiting common-mode rejection the same way it's exploited for field-gradient
sensing?

## Connections to existing skills/papers
- `quantum-sensing` — QFI/CFI/Cramér–Rao machinery, the `H_eff`/`λ(δB)` structure to generalize.
- `coulomb-entanglement` — where the singlet-like ground state / triplet-like excited state actually
  come from (CI on the Hartree product basis); any new coupling operator needs matrix elements in
  this same basis.
- `charge-readout` — the electric-susceptibility/dispersive-shift formalism, relevant if the charge
  channel (see candidate channels in `main.tex`) turns out to be the right one.
- `resonator-coupling` — if any readout of the sensor state itself needs a microwave resonator.

## Open physics questions
- Which candidate channel (parity-switching noise / stray field / direct charge coupling) is
  actually the dominant, detectable one at realistic electron–nanowire distances?
- Order-of-magnitude signal size: what is a reasonable estimate for the stray field or charge
  perturbation an MZM produces at, say, 1–10 µm?
- Quasiparticle poisoning is a stochastic (telegraph-noise-like) process, not a static field — does
  the existing static-parameter QFI/CRB framework even apply, or is this really a parity-readout /
  change-point-detection problem in disguise?
- Is there existing literature on using entangled sensors specifically for topological-qubit parity
  readout that we should be citing/building on (search before writing further)? **Literature check
  done (2026-07-10):** closest precedents found are (i) `vanloo2026kitaev` — real-time, single-shot
  parity readout of a minimal (two-site) Kitaev-chain MZM pair via quantum capacitance, directly
  observing random-telegraph parity switching with lifetimes >1 ms (grounds the *statistics* of the
  target signal, but is an intrinsic/local dispersive probe of the topological device itself, not an
  external differential sensor); (ii) `ramanathan2026parity` — a single superconducting qubit's own
  quasiparticle parity used as a rare-event/dark-matter detector (same "parity flip as particle
  signal" philosophy, but no entanglement and no MZM); (iii) `yelton2025correlated` — measured
  quasiparticle-poisoning statistics (correlated bursts, power-law rate) in conventional
  superconducting qubits, useful as a concrete noise-process model. **No existing proposal found**
  for an external, entangled, common-mode-rejecting sensor pair reading out an MZM signal — this
  project's core idea appears to still be novel, but should be re-checked periodically (fast-moving
  area; Kitaev-chain parity readout was itself only demonstrated in 2025/2026).

## Equations / derivations to work out
- Generalize `H_eff = E_g|g><g| + E_e|e><e| + λ(t)(|g><e|+|e><g|)` for each candidate channel's
  own λ(t) and generator.
- If charge channel: define the analogue of `M_ge` for `(n_L - n_R)` instead of `S^z_L - S^z_R`.
- Redo the QFI derivation (Sec. IV of `perruzza2026`) for whichever channel is chosen.

## Numerics needed
- Extend the CI Hamiltonian (see `ci-dvr-hartree-numerics`) with the new coupling operator once
  chosen. Python first; C++/Fortran (OO) only if a hot kernel emerges. Present in a notebook, e.g.
  `notebooks/07_majorana_sensor_channel_comparison.ipynb`.

## Risks / open challenges
- Physical integration: how would an eHe trap and a topological nanowire actually share a
  cryostat/substrate at the required proximity? Needs input from the experimental side
  (`resonator-coupling`/`charge-readout` device family) on what's realistic.
- Might turn out that none of the three candidate channels give a detectable signal at achievable
  distances — worth stating that as a possible (negative) outcome, not just assuming success.
- Literature check done, see above — no entangled-pair MZM sensor precedent found, but keep
  re-checking; this exact intersection (entangled differential sensing + topological parity) is a
  natural idea and could appear in preprint form at any time.
