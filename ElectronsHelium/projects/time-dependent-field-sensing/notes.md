# Notes — Time-dependent-field sensing for particle physics

Informal brainstorm space. Move stable material into `main.tex`; keep this as the scratch pad.

## Core question
Ref.~perruzza2026 restricts itself to a **static** magnetic-field gradient and explicitly defers
time-dependent fields ("We will address time-dependent fields in future studies"). Can the same
singlet--triplet differential-sensor machinery (QFI/CFI/Cramér–Rao, `H_eff`, generators `G_-`/`G_+`)
be generalized to an oscillating or transient coupling, and which particle-physics target is the best
match once generalized?

## Connections to existing skills/papers
- `quantum-sensing` — the QFI/CFI/CRB machinery to generalize from static `δB` to `δB(t)`.
- `coulomb-entanglement` — where the singlet/triplet states come from; unchanged by this extension.
- `ci-dvr-hartree-numerics` — numerical toolkit; will need time-dependent propagation under the new
  coupling (already used for gate dynamics in `two-qubit-gates`/`leinonen2025`, just a different
  operator).
- `rl-agentic-quantum-control` (sibling project) — reward function would need retargeting from a
  static-gradient CFI reward to an oscillating-signal one.
- `majorana-two-electron-sensor` (sibling project) — same "reuse the differential sensor for a new
  target" pattern, but condensed-matter rather than particle-physics; keep the two projects distinct
  and cross-reference rather than merge.

## Literature search summary (2026-07-08)
Perruzza et al. (arXiv:2606.31910) already qualitatively names, but does not develop, several
particle-physics targets for a future time-dependent extension:
- Light dark matter (Essig et al. 2016; Schutz & Zurek 2016) — sub-eV energy deposition, more of a
  calorimetric/rare-event channel than a coherent oscillating-field channel.
- Axion/ALP dark matter as an oscillating effective Zeeman field (Graham & Rajendran 2013; Abel et al.
  2017; Budker et al. 2014 — CASPEr) — the clearest fit to a `G_+`, common-mode, resonant-narrowband
  extension.
- Entangled/correlated sensor networks for dark matter (Brady et al. 2022; Derevianko 2018) — already
  cited by perruzza2026 as the conceptual basis for its own Sec. 2.9 network outlook.
- Milli-charged particles / hidden-sector bosons as ultrafast transients — impulsive, `G_-`-like
  signal; closer in spirit to a trigger/rare-event search than a coherent-field measurement.

Additional literature identified in this project's search, not yet cited in perruzza2026, narrowing
the "axion/ALP" and "network" targets to specific running/proposed experiments and giving concrete
sensitivity baselines to compare against:
- **ABRACADABRA-10 cm**: Ouellet et al., Phys. Rev. D 99, 052012 (2019) [design]; Salemi et al., Phys.
  Rev. Lett. 127, 081801 (2021) [search, sub-µeV axion mass range].
- **DM Radio pathfinder**: Silva-Feaver, Chaudhuri et al., IEEE Trans. Appl. Supercond. 27, 1400304
  (2017), arXiv:1610.09344 — tunable lumped-element LC resonator, ~100 kHz–10 MHz (hidden photon).
- **GNOME** (Global Network of Optical Magnetometers for Exotic physics searches): Afach et al.,
  Nat. Phys. 17, 1396 (2021) [domain-wall search]; Afach et al., arXiv:2305.01785 (2023) [search-target
  survey] — the clearest existing precedent for a *network* of entangled/correlated spin sensors
  hunting transient dark-matter signatures, directly relevant to perruzza2026 Sec. 2.9.
- **NMR sensitivity to dark photons**: Beadle, Ellis, Leedom & Rodd, arXiv:2505.15897 (2025) —
  shows CASPEr-style apparatus is *also* sensitive to dark photons and the axion-photon coupling, not
  just the axion-nucleon/electron coupling; broadens the "axion" channel into a multi-target one "for
  free."
- **Entangled EDM sensing**: Aoki et al., Quantum Sci. Technol. 6, 044008 (2021) — entangled ultracold
  Fr atoms for electron EDM below 1e-30 e·cm; useful precedent for how an *entanglement advantage* is
  quantified in a precision (not dark-matter) particle-physics context.
- **Exotic spin-dependent ("fifth force") interactions review**: Jiang et al., arXiv:2412.03288 (2024)
  — broad review of spin-sensor searches for BSM short-range forces; likely the lowest-effort
  extension since it stays in the `G_-` gradient channel already built for perruzza2026.
- **Cross-check**: Cecil et al., "Report of the Topical Group on Quantum Sensors for Snowmass 2021,"
  arXiv:2208.13310 (2022) — broad HEP quantum-sensor landscape survey, used to check no obviously
  better-suited existing platform/technique is being missed.

## Open physics questions
- Resonant/narrowband (axion/dark-photon) vs. impulsive/transient (network/domain-wall) vs.
  static-with-oscillating-readout (EDM) — these are three different estimation-theory problems, not
  one. Which is tractable first with the existing QFI/CRB machinery?
- Does the `G_+` (common-mode, Bell/GHZ) channel actually require a network (>2 traps), or can a
  single entangled pair meaningfully probe a spatially uniform oscillating background at all — i.e.,
  what does "differential sensor" even mean for a genuinely common-mode signal, and is the single-pair
  sensitivity gain (if any) coming from a *different* mechanism than the static-gradient factor of 2?
- What eHe-specific frequency/mass window (set by trap baseline, exchange/Zeeman splitting scale,
  coherence time) would be genuinely uncovered by CASPEr/ABRACADABRA/DM Radio/GNOME, versus merely
  duplicating existing coverage with a different physical platform?
- Is the appropriate benchmark "beat existing haloscopes in raw sensitivity" (likely a very high bar
  given decades of dedicated experiment optimization) or "serve as a low-cost, high-coherence
  network node / cross-check," as GNOME-style network searches already do with heterogeneous
  magnetometer types?

## Equations / derivations to work out
- Time-dependent generalization of `H_eff(t) = E_g|g><g| + E_e|e><e| + λ(t)(|g><e|+|e><g|)` for
  `λ(t) = λ_0 cos(ω_a t + φ)` (resonant) and `λ(t) = λ_0 f(t/τ)` (transient).
  - Whether the axion/dark-matter field's own finite coherence time `τ_c ~ 10^6/ω_a` needs to be
    folded into the density matrix (stochastic average over an ensemble of `(δB_0, φ)` realizations)
    rather than treated as a fixed classical drive, as in Ref. graham2013new/budker2014proposal.
- Redo the Fisher information derivation (Sec. IV of perruzza2026) for the amplitude of a known-
  frequency oscillation (matched-filter regime) and, separately, for a transient waveform (change-
  point regime) — likely two distinct appendices rather than one generalized result.
- Define the charge-channel analogue for a dark-photon `(n_L - n_R)` coupling (parallel to the
  charge-coupling channel already sketched in `majorana-two-electron-sensor`).

## Numerics needed
- Language: Python first; C++/Fortran (OO) for hot kernels; present in Jupyter notebooks/Jupyter-book
  (see `skills/ci-dvr-hartree-numerics`, `src/README.md`, `notebooks/README.md`).
- First concrete numerical task once a channel is chosen: propagate the CI two-electron state under
  an oscillating `λ(t)` and compute the time-averaged QFI as a function of `ω_a` and trap baseline,
  reusing the propagation code already used for two-qubit gates (`leinonen2025`).

## Risks / open challenges
- The eHe platform is a new, small-scale device; dedicated haloscopes (ABRACADABRA, DM Radio, CASPEr)
  represent large, mature collaborations with years of systematics control. A credible claim needs to
  be about a specific niche (mass window, network-node role, or entanglement-scaling argument), not
  "beats CASPEr."
- Distinguishing an axion/ALP signal from a dark-photon signal in the same apparatus (per
  beadle2025nmr) is a feature but adds an extra parameter-estimation dimension not present in the
  original static-gradient proposal.
- Literature check ongoing: search again before committing to a specific channel, since this is a
  fast-moving field (note e.g. beadle2025nmr and jiang2024searches are both from 2024/2025 — check for
  2026 follow-ups before finalizing).
