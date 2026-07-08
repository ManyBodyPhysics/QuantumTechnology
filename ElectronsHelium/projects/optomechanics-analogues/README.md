# Optomechanical analogues for electrons on helium

**Status:** idea / outline, with the central feasibility question now partly resolved by new
experimental data (see below). No protocol has itself been simulated or demonstrated yet — see
`main.tex` for the motivating introduction and outlined model (sideband cooling, motional squeezing,
motional entanglement), and `notes.md` for the literature-update summary and open-questions scratch
pad.

**Pitch:** an electron on helium dipole-coupled to a microwave resonator is formally a
cavity-optomechanical system. Three landmark optomechanics protocols — sideband cooling
(Teufel et al. 2011), motional squeezing (Pirkkalainen et al. 2015), and dissipative
(reservoir-engineered) motional entanglement between two oscillators (Ockeloen-Korppi et al. 2018) —
have not, to our knowledge, been translated to this platform. Their shared prerequisite, single-
electron strong coupling to a microwave photon, has now been **experimentally demonstrated on this
exact platform**: Koolstra et al., *Strong coupling of a microwave photon to an electron on helium*,
Nat. Phys. (2026) — [DOI: 10.1038/s41567-026-03342-z](https://doi.org/10.1038/s41567-026-03342-z),
PDF at `papers/2026_Kolstra_naturephysics.pdf`, bib key `koolstra2026strong` (preprint
`koolstra2025strong`, arXiv:2509.14506) — reports $g/2\pi = 118\pm3$ MHz, $\kappa/2\pi = 23$ MHz,
electron decoherence as low as $\Gamma_2/2\pi = 61$ MHz, a single-photon cooperativity
$\mathcal{C} = 4g^2/(\kappa\Gamma_2) \approx 32$, and operation down to 7 mK — putting the device
deep in the resolved-sideband ($\kappa/\omega_e \sim 3\times10^{-3}$), high-cooperativity regime this
project's three protocols require. This project now asks which figure of merit (final phonon
occupation, squeezing in dB, entanglement negativity) each protocol actually achieves given these
measured parameters — and, for the entanglement case, how a dissipative, resonator-mediated
entangling mechanism compares to the existing, coherent, direct-Coulomb mechanism already used on
this platform (`coulomb-entanglement`).

**Target journal:** TBD — Phys. Rev. Applied or Phys. Rev. A are plausible; `main.tex` class options
default to `prapplied`.

**Related skills:** `resonator-coupling`, `charge-readout` (design-stage device parameters),
`coulomb-entanglement` (comparison point for the entanglement protocol),
`ci-dvr-hartree-numerics` (would need a Lindblad/dissipative extension). `koolstra2026strong` is not
yet promoted to its own skill — tracked in this project's `notes.md`/`references.bib` for now.

**First concrete task:** the resolved-sideband/cooperativity budget is now answered ($\mathcal{C}
\approx 32$, resolved sideband, per `koolstra2026strong`); the next step is computing the actual
final-phonon-occupation and squeezing-in-dB figures of merit using the measured, temperature-dependent
(non-saturating, dephasing-dominated) $\Gamma_2(T)$ curve rather than a single fixed decoherence rate
— see `notes.md`. The entanglement protocol remains the least-constrained of the three, since
`koolstra2026strong` demonstrates single-electron, single-dot strong coupling only, not a
two-electron shared-resonator device.
