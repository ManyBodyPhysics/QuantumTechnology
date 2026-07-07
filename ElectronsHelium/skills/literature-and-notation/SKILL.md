---
name: literature-and-notation
description: >-
  The project's shared reference desk: consistent symbol/notation conventions, the natural-unit
  systems and physical constants used across the electrons-on-helium papers, a "which paper proves
  which result" map, and the curated BibTeX database (references.bib) including the five core papers.
  Use this skill whenever the user writes or edits a manuscript, abstract, or notebook for this
  project and needs consistent notation/units; whenever they ask "where did we show X?", "what's our
  convention for Y?", or need a citation/BibTeX key; or when starting new work that must line up with
  the existing five papers. Consult it to prevent notation drift and mismatched numbers across the
  program.
---

# Literature & notation reference desk

Use this to keep every new manuscript, notebook, and skill consistent with the five core papers.
When in doubt about a symbol, unit, number, or citation, check here rather than guessing.

## What to read when

- **Symbols, units, constants, sign conventions** → `references/notation.md`.
- **Which paper contains which result / model / figure** → `references/paper-map.md`.
- **BibTeX** → `references/references.bib` (88 entries; includes the five core papers as
  `perruzza2026`, `leinonen2025` [PRA gates], `beysengulov2024` [PRX entanglement],
  `koolstra2025impedance` [PRApplied resonator design], `castoria2025` [PRX charge sensing]).

## The five core papers (cite these keys)

Three **theory** papers share one device/CI backbone (Oslo group); two **experimental** papers
(EeroQ Corporation collaboration) demonstrate the microwave-resonator readout hardware. Keep the two
device families distinct — see the "Cross-cutting threads" note in `references/paper-map.md`.

- `beysengulov2024` — *Coulomb Interaction-Driven Entanglement of Electrons on Helium*, PRX Quantum
  **5**, 030324 (2024). Entanglement generation, Hartree/CI, configurations I/II/III. →
  `skills/coulomb-entanglement`.
- `leinonen2025` — *Design and dynamics of two-qubit gates with motional states of electrons on
  helium*, Phys. Rev. A **113**, 032624 (2026). √iSWAP/CZ gate protocols, propagation, fidelity,
  screening/decoherence. → `skills/two-qubit-gates`.
- `perruzza2026` — *Electrons on Helium and Entangled Quantum Sensors for Particle Physics* (2026,
  DRD5). Entangled singlet–triplet sensor, Fisher information, RL, sensor networks. →
  `skills/quantum-sensing`.
- `koolstra2025impedance` — *High-Impedance Resonators for Strong Coupling to an Electron on Helium*,
  Phys. Rev. Appl. **23**, 024001 (2025). SCR circuit design, TiN fabrication, coupling-strength
  roadmap toward strong coupling. → `skills/resonator-coupling`.
- `castoria2025` — *Sensing and Control of Single Trapped Electrons above 1 K*, Phys. Rev. X **15**,
  041002 (2025). Dispersive charge sensing, deterministic single-electron loading/control,
  elevated-temperature (>1 K) operation. → `skills/charge-readout`.

## Quick consistency checklist (apply to any new text)

- Natural units `ℏ²/2mₑ = 1`, `ℏ = 1` stated explicitly; give ≥1 conversion to physical units.
- Soft Coulomb `u = κ/√((x₁−x₂)²+ε²)`, `κ = 2326`, `ε = 1e-2`; energy unit `E_d = ℏ²/(mₑx₀²)`,
  `x₀ = 123 nm`.
- Device: 7 electrodes (200 nm wide / 200 nm spacing), He depth `h = 500 nm`, electron separation
  `d ≈ 1.5 µm`, level spacings `5–15 GHz`.
- Configurations named **I (idle) / II (iSWAP-type) / III (CZ-type)**; ZZ coupling
  `ζ = E₄ − E₂ − E₁ + E₀`.
- Sensing: `δB = B_L − B_R`, `M_ge = ⟨e|S^z_L − S^z_R|g⟩`, `Δ_ST = E_e − E_g`; QFI gain for the ideal
  pair is a **factor of 2** (= N=2 Heisenberg), network `1/N` is a proposal.
- Coherence numbers: label spin-coherence figures as **predicted**; keep a single consistent value
  within a manuscript.
- Author list / affiliations for the sensing paper: see `references/paper-map.md`.
- Resonator/readout: coupling `g = ½eE_xω₀√(Z_res/m_eω_e)`; dispersive shift
  `Δf ≈ −f_rRe[χ_e(2πf_r)]/2`, `χ_e(ω)=Σ_n4g_n²/(ω_n²−ω²+2iωΓ_n)`. These come from a **different
  (EeroQ) device family** than the Oslo 7-electrode geometry above — don't mix the two.

## Guidance

- Prefer the existing symbol set over inventing new ones; if a new quantity is needed, define it once
  and add it to `references/notation.md`.
- When citing, reuse the keys above so bibliographies stay consistent across notebooks and papers.
