# Notes — Optomechanical analogues for electrons on helium

Informal brainstorm space. Move stable material into `main.tex`; keep this as the scratch pad.

## Core question
Can the three landmark optomechanics protocols (sideband cooling, motional squeezing, dissipative
motional entanglement) be translated onto the eHe electron-motion + resonator system, using the
device parameters now demonstrated by `resonator-coupling` and `charge-readout`?

## Connections to existing skills/papers
- `resonator-coupling` — the coupling formula, measured `Z_res`, `Q_i`, `κ_i`; this is where the
  cooperativity budget's *design* numbers originally came from, now superseded for the strong-coupling
  device by the *measured* numbers in `koolstra2026strong` (see literature update below).
- `charge-readout` — measured `g_e/2π = 9.8 MHz`, operating temperature 1.1 K, thermal-occupation
  context (this device is warm — good for charge counting, not the device to use for the
  cooling/squeezing budget; `koolstra2026strong` is a separate, colder, more strongly coupled device).
- `koolstra2026strong` (new) — the strong-coupling demonstration this project's cooling/squeezing
  sections now build on directly; not yet promoted to its own skill, tracked here and in
  `main.tex`/`references.bib` for now.
- `coulomb-entanglement` — the existing, coherent, direct-Coulomb entanglement mechanism to compare
  against the proposed dissipative (reservoir-engineered) mechanism.
- `ci-dvr-hartree-numerics` — would need extending with cavity dissipation (Lindblad) for any of
  the three protocols to be simulated quantitatively; this is currently flagged as unbuilt.

## Literature update (2026-07-08): Koolstra et al., Nat. Phys. (2026) — strong coupling demonstrated
`koolstra2026strong` ("Strong coupling of a microwave photon to an electron on helium," Nat. Phys.,
published 15 June 2026; PDF in `papers/2026_Kolstra_naturephysics.pdf`; preprint
`koolstra2025strong` = arXiv:2509.14506) reports the **first experimental strong-coupling
demonstration** on exactly this platform, superseding the design/projection numbers this project's
`main.tex` previously relied on. Key measured parameters (vacuum Rabi splitting fit, single-electron
device):
- Coupling rate `g/2π = 118 ± 3 MHz` (vacuum Rabi fit) / `110 MHz` (two-tone spectroscopy, broad
  voltage range) — matches the `koolstra2025impedance` design value and *exceeds* the
  `g/2π ≈ 80 MHz` projection this project's `main.tex` previously flagged as a needed future
  improvement.
- Resonator linewidth `κ/2π = 23 MHz` (loaded, from transmission fit — this is the number to use for
  the cooperativity/sideband budget, not the `κ_i/2π = 11.7 kHz` internal-only figure from
  `koolstra2025impedance`).
- Electron decoherence `Γ2/2π = 75 ± 5 MHz` (vacuum Rabi fit), improving to `Γ2/2π = 61 MHz` (best
  measured, with negative electrode voltage offset ΔV).
- Single-photon cooperativity `C = 4g²/(κΓ2) ≈ 32` — reported directly in the paper.
- Electron motional frequency tunable `ωe/2π ≈ 5.5–8.7 GHz`; resonator `ωr/2π = 7.162 GHz`.
- `κ/ωe ~ 3×10⁻³ ≪ 1` — device is deep in the resolved-sideband regime.
- Energy relaxation `T1 ≈ 0.76 μs` (large detuning); decoherence is dephasing-dominated
  (`γ1 ≪ Γ2`, i.e. `Γ2 = γ1/2 + γφ ≈ γφ`).
- `Γ2` follows a `T^0.5` power law from 7 mK to 450 mK, no saturation at lowest T — tentatively
  ripplon- or stray-charge-limited, not yet fully understood.
- Device operated in a dilution refrigerator down to 7 mK (not the 1.1 K regime of `castoria2025`).
- The paper's own outlook explicitly anticipates "exotic ultrastrong coupling regimes of circuit
  quantum optics" as a next step — directly overlapping with this project's framing — though its
  stated near-term follow-up is spin readout via spin–orbit hybridization (micromagnet + field
  gradient), not the cooling/squeezing/entanglement protocols pursued here.

**Effect on this project's open questions (see below): the resolved-sideband and cooperativity
prerequisites are now answered (yes, with margin); the actual figures of merit (final phonon
occupation, squeezing in dB, entanglement negativity) still need to be computed.**

## Open physics questions
- ~~Resolved-sideband regime check: is `κ ≪ ω_e` satisfied for either demonstrated device?~~
  **Resolved**: yes, `κ/ωe ~ 3×10⁻³` per `koolstra2026strong`.
- ~~Cooperativity `C = 4g²/(κΓ)`: compute for both devices' demonstrated parameters.~~ **Resolved**:
  `C ≈ 32` per `koolstra2026strong` (using the strong-coupling device, not the `castoria2025`
  dispersive-readout device).
- ~~Thermal occupation at 1.1 K vs. mK~~ **Partly resolved**: `koolstra2026strong` operates down to
  7 mK, giving `n̄ ≪ 1` for a ~7–9 GHz mode without active cooling — still need the actual squeezing/
  cooling figure of merit given the measured (non-saturating, dephasing-dominated) `Γ2(T)`.
- **New/sharpened question**: does the observed `T^0.5`, non-saturating dephasing impose a cooling/
  squeezing ceiling below what `C ≈ 32` alone would suggest via the standard formulas? This requires
  using the measured `Γ2(T)` curve, not a single number, in the cooling/squeezing figure-of-merit
  calculation.
- Dissipative two-electron entanglement: does it need a *shared* resonator mode (both electrons in
  the same trap/dot) or can it work with two separate, coupled resonators for spatially separated
  electrons? The latter would be the more interesting/novel case (cf. sensor networks in
  `quantum-sensing`). **Still fully open** — `koolstra2026strong` is single-electron, single-dot only;
  no two-electron shared-resonator device exists yet to ground this calculation in.

## Equations / derivations to work out
- Full (non-RWA) linearized Hamiltonian and the conditions under which the RWA sideband picture in
  `main.tex` is valid for this specific system (check against `koolstra2026strong`'s actual `g`,
  `ω_r`, `ω_e` values — now measured, not projected).
- Cooperativity and final-phonon-occupation formulas (standard optomechanics results, see
  `aspelmeyer2014cavity` for the general expressions) evaluated with the `koolstra2026strong` device
  numbers (`g/2π=118 MHz`, `κ/2π=23 MHz`, `Γ2/2π=61–75 MHz`, `C≈32`).
- Redo the final-phonon-occupation and squeezing-in-dB formulas using the measured `Γ2(T) ∝ T^0.5`
  curve (7 mK–450 mK) rather than a single fixed `Γ2`, to check whether the non-saturating dephasing
  caps performance at low T.
- Two-mode squeezing level in dB as a function of drive detuning ratio and `C`.
- Steady-state entanglement (logarithmic negativity) for the driven-dissipative two-electron case —
  this needs a Lindblad master equation, not just the closed-system CI machinery currently in
  `ci-dvr-hartree-numerics`, and a two-electron shared-resonator device design that does not yet exist
  in the experimental literature.

## Numerics needed
- Python first for the cooperativity/occupation/squeezing formula evaluation (closed-form, no heavy
  numerics needed for a first pass — and now has real numbers to evaluate against, from
  `koolstra2026strong`). A Lindblad solver (QuTiP or a custom implementation) would be needed for the
  entanglement steady-state calculation — flag whether this belongs in `src/eoh/` as a new module
  (e.g. `src/eoh/optomechanics.py`) or is out of scope for a first pass using known closed-form
  cooperativity results. Present in a notebook, e.g.
  `notebooks/09_optomechanics_feasibility.ipynb`.

## Risks / open challenges
- With `C≈32` and resolved sideband now demonstrated, "not yet feasible with demonstrated hardware"
  is no longer the most likely first-pass outcome for cooling/squeezing — but the non-saturating,
  dephasing-dominated `Γ2(T)` is a real, measured complication the standard formulas don't
  automatically account for; don't assume `C≈32` alone guarantees good performance without working
  through the temperature dependence.
- The entanglement protocol (Sec. `\ref{sec:entanglement}` in `main.tex`) has no experimental
  single-electron-pair strong-coupling precedent yet — `koolstra2026strong` is single-dot only. Don't
  overstate how close this makes the entanglement channel to being tested; it mainly de-risks the
  *per-electron* coupling physics the two-electron extension would build on.
- Keep the "in-house" Massel connection (see `main.tex` intro) as a factual note, not an argument for
  feasibility — shared authorship doesn't make the physics work out.
