---
name: quantum-dots-primer
description: >-
  Background primer on semiconductor quantum dots (QDs) and double quantum dots (DQDs) as the
  solid-state analog of the electrons-on-helium platform: three-dimensional confinement and
  atom-like levels, charge and spin qubits, singlet–triplet (S–T₀) qubits, exchange, ZZ coupling,
  and the properties (fast scintillation, tunable spectra, mature fabrication) that make QDs
  relevant both as detector materials and as a comparison point. Use this skill whenever the user
  mentions quantum dots, double quantum dots, singlet-triplet qubits, semiconductor spin qubits,
  exchange coupling, or asks how the eHe results map onto / differ from quantum-dot physics — and
  whenever a proposal or paper needs an accurate, fair QD comparison paragraph.
---

# Quantum dots & double quantum dots (the solid-state analog)

This skill supplies the quantum-dot context that the eHe work repeatedly leans on. The eHe
double-well maps closely onto a **double quantum dot (DQD)**; keep the analogy precise, and keep the
*differences* honest.

## What a quantum dot is

A quantum dot is a nanoscale semiconductor structure that confines carriers in all three spatial
dimensions, producing discrete, atom-like energy levels ("artificial atom"). Level spacings and
spectra are tunable through **size, composition, and gate voltages**. QDs are a mature technology
originally developed for optoelectronics and imaging, valued for **fast scintillation response,
narrow/tunable emission lines**, and high-fidelity electrical control.

## Qubit encodings (know which one is meant)

- **Charge qubit** — position/orbital state of an electron in a DQD (which dot). Fast, easy to
  read, but noisy (couples strongly to charge noise).
- **Single-spin (Loss–DiVincenzo) qubit** — the spin of one confined electron; long-lived,
  controlled by ESR/EDSR, read by spin-to-charge conversion.
- **Singlet–triplet (S–T₀) qubit** — encoded in the two-electron `{|S⟩, |T₀⟩}` subspace of a DQD.
  Driven by the **exchange** `J` (detuning ε) and by a **magnetic-field gradient** `δB` between the
  dots. This is the encoding most directly analogous to the eHe sensing proposal; see
  `quantum-sensing`.

### The S–T₀ two-level structure (shared with the eHe sensor)

For two spins with local Zeeman fields `B_L, B_R`, write `B̄=(B_L+B_R)/2`, `δB=B_L−B_R`:

- The **uniform** field `B̄` shifts the triplet manifold by total `S^z` but does **not** mix
  `|S⟩` and `|T₀⟩`.
- The **gradient** `δB` is antisymmetric under L↔R and **couples** `|S⟩ ↔ |T₀⟩` with matrix element
  `⟨T₀|H_B|S⟩ = gµ_B δB / 2`, since `(S^z_L − S^z_R)|S⟩ = |T₀⟩`.

This is exactly the mechanism the eHe sensor uses — the difference is that in a DQD the two-electron
coupling comes from **exchange (wavefunction overlap)**, whereas on helium it comes from
**Coulomb interaction without exchange** (barrier suppresses tunnelling). Say this explicitly when
drawing the analogy.

## Exchange and ZZ coupling

- **Exchange `J`** splits singlet and triplet and is the native two-qubit knob in gated DQDs;
  tuned by interdot detuning/barrier.
- **ZZ coupling** `ζ = E₄ − E₂ − E₁ + E₀` measures the shift in one qubit's transition when the
  other is excited. It is an unwanted phase-error source in most gates but is *deliberately used* to
  build a CZ in configuration III. Suppressing ζ (e.g. via **opposite-sign anharmonicities**
  `β_L = −β_R`, or by direct minimization) improves swap-type gate fidelity. The eHe gate work
  inherits this superconducting-qubit design language — see `two-qubit-gates` and `coulomb-entanglement`.

## Why QDs appear in the sensing story

- As **detector materials**: proposals embed QDs in calorimeters using "chromatic" scintillation to
  improve energy resolution and particle ID.
- As a **comparison platform** for entangled sensing: semiconductor S–T₀ qubits and NV centers
  already demonstrate entanglement-enhanced magnetometry; eHe is pitched as a cleaner-environment
  alternative with potentially longer coherence and greater uniformity.

## Fair-comparison checklist (use in intros/discussions)

| Axis | Quantum dots | Electrons on helium |
|---|---|---|
| Confinement | 3D in solid; gate-tunable | image potential (z) + electrostatic (in-plane) |
| Two-qubit coupling | exchange (overlap) + Coulomb | Coulomb, **no exchange** (barrier) |
| Environment | host lattice; charge/nuclear-spin noise (mitigated by isotopic purification) | defect-free vacuum above liquid; no nuclear spins |
| Coherence | ms–s (spin, isotopically purified Si) | predicted very long spin coherence (unmeasured) |
| Maturity | high (fabrication, control, readout) | emerging (single-electron control demonstrated) |
| Radiation hardness | limited by solid-state defects | intrinsically higher (floats above liquid) |

Keep the table's claims calibrated: QD maturity is real and demonstrated; several eHe advantages are
predicted. See `platform-electrons-on-helium` for the eHe side and `literature-and-notation` for
citations.
