# Two electrons on helium as a differential sensor for Majorana zero modes

**Status:** idea / outline. No results yet — see `main.tex` for the motivating introduction and
outlined model, and `notes.md` for the open-questions scratch pad.

**Pitch:** the singlet differential-sensor scheme built for particle-physics field-gradient sensing
(`perruzza2026`, `quantum-sensing` skill) is, in principle, agnostic to what local signal it's
rejecting a common mode against. This project asks whether it can be repurposed to detect a local
signature of a Majorana zero mode in a nearby topological superconductor — three candidate signal
channels are outlined in `main.tex` (parity-switching noise, stray field from Majorana-induced
edge/Andreev currents, direct charge coupling), none yet evaluated for feasibility.

**Target journal:** TBD — Phys. Rev. A or PRX Quantum are plausible given the sensing-paper
precedent; the `main.tex` class options are set up for either.

**Related skills:** `quantum-sensing` (QFI/CFI/CRB machinery to extend), `coulomb-entanglement`
(where the entangled states come from), `charge-readout` (if the charge-coupling channel is chosen),
`resonator-coupling` (if sensor readout needs a resonator).

**First concrete task:** narrow the three candidate signal channels in `main.tex` Sec.~II.B down to
one, with an order-of-magnitude signal-size estimate, before attempting any QFI calculation.
