# Notes — Optomechanical analogues for electrons on helium

Informal brainstorm space. Move stable material into `main.tex`; keep this as the scratch pad.

## Core question
Can the three landmark optomechanics protocols (sideband cooling, motional squeezing, dissipative
motional entanglement) be translated onto the eHe electron-motion + resonator system, using the
device parameters now demonstrated by `resonator-coupling` and `charge-readout`?

## Connections to existing skills/papers
- `resonator-coupling` — the coupling formula, measured `Z_res`, `Q_i`, `κ_i`; this is where the
  cooperativity budget's numbers come from.
- `charge-readout` — measured `g_e/2π = 9.8 MHz`, operating temperature 1.1 K, thermal-occupation
  context (this device is warm — good for charge counting, likely bad for squeezing without
  cooling first).
- `coulomb-entanglement` — the existing, coherent, direct-Coulomb entanglement mechanism to compare
  against the proposed dissipative (reservoir-engineered) mechanism.
- `ci-dvr-hartree-numerics` — would need extending with cavity dissipation (Lindblad) for any of
  the three protocols to be simulated quantitatively; this is currently flagged as unbuilt.

## Open physics questions
- Resolved-sideband regime check: is `κ ≪ ω_e` satisfied for either demonstrated device? Need actual
  numbers for the *loaded* linewidth (not just internal `κ_i`), and the electron motional frequency
  `ω_e` at realistic trap curvatures.
- Cooperativity `C = 4g²/(κΓ)`: compute for both devices' demonstrated parameters and see how far
  from `C ≥ 1` (or `C ≫ 1` for good cooling/squeezing) they are.
- Thermal occupation at 1.1 K vs. mK: is squeezing/cooling even meaningful to discuss for the
  Castoria device's operating point, or does this protocol fundamentally require the mK regime?
- Dissipative two-electron entanglement: does it need a *shared* resonator mode (both electrons in
  the same trap/dot) or can it work with two separate, coupled resonators for spatially separated
  electrons? The latter would be the more interesting/novel case (cf. sensor networks in
  `quantum-sensing`).

## Equations / derivations to work out
- Full (non-RWA) linearized Hamiltonian and the conditions under which the RWA sideband picture in
  `main.tex` is valid for this specific system (check against actual `g`, `ω_r`, `ω_e` values).
- Cooperativity and final-phonon-occupation formulas (standard optomechanics results, see
  `aspelmeyer2014cavity` for the general expressions) evaluated with eHe device numbers.
- Two-mode squeezing level in dB as a function of drive detuning ratio and `C`.
- Steady-state entanglement (logarithmic negativity) for the driven-dissipative two-electron case —
  this needs a Lindblad master equation, not just the closed-system CI machinery currently in
  `ci-dvr-hartree-numerics`.

## Numerics needed
- Python first for the cooperativity/occupation/squeezing formula evaluation (closed-form, no heavy
  numerics needed for a first pass). A Lindblad solver (QuTiP or a custom implementation) would be
  needed for the entanglement steady-state calculation — flag whether this belongs in `src/eoh/` as
  a new module (e.g. `src/eoh/optomechanics.py`) or is out of scope for a first pass using known
  closed-form cooperativity results. Present in a notebook, e.g.
  `notebooks/09_optomechanics_feasibility.ipynb`.

## Risks / open challenges
- The most likely outcome of a first pass is "not yet feasible with demonstrated hardware, feasible
  with the projected narrower-wire device" — that's a legitimate, useful result; don't force a more
  optimistic conclusion.
- Keep the "in-house" Massel connection (see `main.tex` intro) as a factual note, not an argument for
  feasibility — shared authorship doesn't make the physics work out.
