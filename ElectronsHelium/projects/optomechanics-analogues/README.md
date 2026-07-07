# Optomechanical analogues for electrons on helium

**Status:** idea / outline. No results yet — see `main.tex` for the motivating introduction and
outlined model (sideband cooling, motional squeezing, motional entanglement), and `notes.md` for the
open-questions scratch pad.

**Pitch:** an electron on helium dipole-coupled to a microwave resonator is formally a
cavity-optomechanical system. Three landmark optomechanics protocols — sideband cooling
(Teufel et al. 2011), motional squeezing (Pirkkalainen et al. 2015), and dissipative
(reservoir-engineered) motional entanglement between two oscillators (Ockeloen-Korppi et al. 2018) —
have not, to our knowledge, been translated to this platform. With demonstrated coupling-strength
engineering (`resonator-coupling`) and demonstrated dispersive readout (`charge-readout`) now in
hand, this project asks which of the three is feasible with real device parameters, and — for the
entanglement case — how a dissipative, resonator-mediated entangling mechanism compares to the
existing, coherent, direct-Coulomb mechanism already used on this platform (`coulomb-entanglement`).

**Target journal:** TBD — Phys. Rev. Applied or Phys. Rev. A are plausible; `main.tex` class options
default to `prapplied`.

**Related skills:** `resonator-coupling`, `charge-readout` (device parameters for the feasibility
budget), `coulomb-entanglement` (comparison point for the entanglement protocol),
`ci-dvr-hartree-numerics` (would need a Lindblad/dissipative extension).

**First concrete task:** a cooperativity and sideband-resolution budget using the actual measured
parameters from `resonator-coupling` and `charge-readout`, to see which (if any) of the three
protocols is feasible with demonstrated hardware today — see `notes.md`.
