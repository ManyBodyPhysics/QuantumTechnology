---
name: platform-electrons-on-helium
description: >-
  Foundational physics primer for the electrons-on-helium (eHe) quantum platform: how single
  electrons are trapped above superfluid helium, the Rydberg-like out-of-plane spectrum, in-plane
  electrostatic double-well confinement, cQED/image-charge readout, coherence times, and how the
  platform compares with semiconductor quantum dots and solid-neon electrons. Use this skill
  whenever the user works on electrons on helium, eHe qubits, trapped surface electrons, "electrons
  on liquid helium", ripplon coupling, the DRD5 sensor context, or asks for background/orientation
  before diving into entanglement, gates, or sensing on this platform. Consult it even when the
  request is phrased casually (e.g. "remind me how the helium trap works", "what sets coherence on
  eHe?") — it holds the shared physical picture the other skills build on.
---

# Platform: electrons on superfluid helium (eHe)

This is the shared physical foundation for the whole project. The gate, entanglement, and sensing
skills all assume the picture below. Read this first when orienting; then branch to the specialized
skill (`coulomb-entanglement`, `two-qubit-gates`, `quantum-sensing`, `quantum-dots-primer`) and to
`ci-dvr-hartree-numerics` for computation and `literature-and-notation` for symbols/units.

## The one-paragraph picture

A single electron placed in vacuum above a cryogenic superfluid-⁴He film is pulled toward the
surface by its own image charge in the dielectric, but is blocked from entering the liquid by a
large (~1 eV) Pauli barrier at the vapor–liquid interface. The balance produces a **Rydberg-like
ladder of quantized states for the out-of-plane (z) motion**, with the electron sitting ~10 nm above
the surface in the ground state at low temperature. Lateral (in-plane) motion is confined and shaped
by voltages on **micro-fabricated electrodes beneath the helium**, forming tunable single- or
double-well traps. Because there is no host lattice, the environment is exceptionally clean: no
crystal defects, no stray nuclear spins, and weak coupling to the only intrinsic bath (surface
capillary waves = **ripplons**). This underlies the platform's long predicted coherence.

## Key physical facts to keep consistent

- **Two quantized sectors.** (i) Out-of-plane Rydberg states set by the image potential; the
  electron is initialized to the ground state for `T < 2 K`. (ii) In-plane motional states set by
  the electrostatic trap, engineered into the microwave range (`5–15 GHz` level spacings along the
  principal `x` axis; the orthogonal `y` axis is stiffer, ~6× higher frequency, and often treated as
  frozen to first approximation — but full 2D treatments are used when accuracy matters).
- **Interaction knob.** Two electrons in neighbouring wells interact by (largely **unscreened**)
  **Coulomb repulsion**. This is the entangling resource — analogous to a double quantum dot but
  *without* wavefunction-overlap/exchange, since the barrier suppresses tunnelling.
- **Readout.** Motional/charge state is read dispersively via a superconducting microwave resonator
  (electron shifts resonator frequency; vacuum Rabi splitting on resonance) and via **image-charge
  sensing** (Rydberg transitions induce a current pulse in a cryogenic amplifier). This is not just a
  qualitative picture: `resonator-coupling` gives the circuit engineering for the coupling strength `g`
  (high-impedance SCR design, TiN fabrication, a roadmap toward strong coupling), and `charge-readout`
  demonstrates actual dispersive electron counting and deterministic single-electron loading/control
  — at `T = 1.1 K`, well above typical mK cQED. Both are from a **separate EeroQ-collaboration device
  family**, distinct from the Oslo 7-electrode geometry used elsewhere in this project. Spin readout is
  not yet native — it is envisaged via **spin-to-charge conversion** (map spin onto orbital with a
  magnetic gradient, then read the charge/motion). Treat spin readout as an open experimental
  problem, not a solved capability, even though charge/orbital readout is now well demonstrated.
- **Coherence.** Motional/orbital coherence has been discussed well above milliseconds; **electron
  *spin* coherence is predicted to be very long** (theory estimates range from ≳ seconds up to
  ~100 s in the cleanest limit). When quoting a number, cite the source and note it is a *prediction*
  — measured spin coherence on eHe is not yet established. The dominant near-term motional-dephasing
  channel in current experiments is charge/dephasing noise on the order of tens of MHz.
- **Ripplons.** The intrinsic bath is quantized surface capillary waves. Single-ripplon *decay* of
  motional states is strongly suppressed (momentum mismatch), but ripplons can *dephase* motional
  states; the coupling is tunable by the vertical pressing field `E⊥`, moving between strong- and
  weak-coupling regimes (a narrow zero-ripplon line appears in the weak-coupling regime, analogous
  to a zero-phonon line).

## Device geometry (shared across the three core papers)

- A silicon chip carries a linear array of gate electrodes (commonly **7 electrodes, 200 nm wide,
  200 nm spacing**) beneath a ~500 nm superfluid-He layer, producing an electrostatic **double-well**
  for two electrons separated by **≈ 1.5 µm**.
- Each electron is dipole-coupled (`g`) to its own microwave cavity for single-qubit control/readout;
  the two electrons couple to each other through Coulomb `κ`.
- The trap shape is set by a **voltage vector** `V = {V₁,…,V₇}`; interpolating `V(λ)=(1-λ)V_I+λV_III`
  moves between named **configurations I / II / III** (idle / iSWAP-type / CZ-type). This
  parametrization is the bridge to both the gate work and the sensing work.

## Why this platform (framing for proposals and intros)

- **Pristine environment** → long coherence, high uniformity, intrinsic radiation-hardness relative
  to solid-state qubits (electrons float above a defect-free liquid; no nuclear spins).
- **Cryo-native** → compatible with dilution-refrigerator/superconducting-magnet infrastructure that
  particle-physics and dark-matter experiments already run.
- **Scalable fabrication** → CMOS-compatible traps; single-electron loading, shuttling, and control
  have been demonstrated experimentally.
- **Complementary to quantum dots** → QDs bring mature nanofabrication and gate-tunability; eHe
  brings the near-dissipation-free vacuum environment. Keep both in view (see `quantum-dots-primer`).

## When writing or reviewing text on this platform

- Distinguish **demonstrated** (single-electron trapping/shuttling/control, strong charge–photon
  coupling, dispersive charge readout above ~1 K) from **predicted/proposed** (long spin coherence,
  spin readout, two-qubit gates, entangled sensing). Don't let a proposal's aspirations read as
  achieved results.
- Keep numbers internally consistent across a manuscript (coherence times, level spacings, electrode
  counts, separation). Cross-check against `literature-and-notation`.
- Natural units are used pervasively (`ℏ²/2mₑ = 1`, `ℏ = 1`); state the convention explicitly and
  give at least one conversion to physical units (T, ns, µm) for readers. See `literature-and-notation`.

## Pointers

- Entanglement generation and the CI machinery → `coulomb-entanglement`.
- Gate protocols (√iSWAP, CZ), pulse shaping, fidelity → `two-qubit-gates`.
- Field/particle sensing (singlet–triplet, Fisher information, networks) → `quantum-sensing`.
- Resonator/impedance engineering for electron–photon coupling → `resonator-coupling`.
- Demonstrated dispersive charge sensing and single-electron control → `charge-readout`.
- Numerics (DVR, Hartree, CI, propagation, RL) → `ci-dvr-hartree-numerics`.
- Symbols, units, `references.bib`, "which paper has which result" → `literature-and-notation`.
- Full source papers: `papers/` (PDFs) and `papers/summaries/` (structured markdown).
