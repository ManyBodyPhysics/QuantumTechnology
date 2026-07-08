# Beyond the static gradient: electrons on helium as a time-dependent-field sensor for particle physics

**Status:** idea / outline. No results yet — see `main.tex` for the motivating introduction and
outlined model, and `notes.md` for the literature-search summary and open-questions scratch pad.

**Pitch:** `perruzza2026` deliberately limited its entangled singlet--triplet sensor to a *static*
magnetic-field gradient, stating explicitly that time-dependent fields are future work. This project
takes up that extension: generalize the sensor Hamiltonian $H_{\rm eff}(t)$ and the QFI/CFI/Cramér–Rao
machinery to an oscillating or transient coupling, and use a literature survey of running/proposed
particle-physics experiments to identify which target — oscillating axion/ALP dark matter, dark
photons, network-based transient/domain-wall searches, or electric-dipole-moment precision
measurements — is the best match for the platform's trap geometry, coherence budget, and $G_-$
(gradient) / $G_+$ (common-mode) readout modes. Five candidate channels are outlined in `main.tex`
Sec.~III, none yet evaluated for quantitative feasibility against existing experiments' sensitivity
curves.

**Target journal:** TBD — PRX Quantum or Phys. Rev. A are plausible given the sensing-paper
precedent; the `main.tex` class options are set up for either.

**Related skills:** `quantum-sensing` (QFI/CFI/CRB machinery to extend to time-dependent couplings),
`coulomb-entanglement` (where the entangled states come from), `ci-dvr-hartree-numerics` (propagation
under the new time-dependent operator).

**Related projects:** `majorana-two-electron-sensor` (same differential-sensor-repurposing pattern,
condensed-matter rather than particle-physics target — kept distinct, cross-referenced);
`rl-agentic-quantum-control` (trap-optimization reward would need retargeting from the static-gradient
CFI reward to an oscillating-signal one, once a channel is chosen).

**Literature search (2026-07-08):** see `notes.md` for the full summary. Key sources beyond what
`perruzza2026` already cites: ABRACADABRA-10\,cm (Ouellet et al. 2019; Salemi et al. 2021), the DM
Radio pathfinder (Silva-Feaver, Chaudhuri et al. 2017), the GNOME network (Afach et al. 2021, 2023),
a 2025 result showing CASPEr-style NMR apparatus is also sensitive to dark photons (Beadle, Ellis,
Leedom & Rodd), an entangled-atom electron-EDM proposal (Aoki et al. 2021), a review of exotic
spin-dependent ("fifth-force") interaction searches (Jiang et al. 2024), and the Snowmass 2021
quantum-sensors topical-group report (Cecil et al. 2022) as a broader cross-check.

**First concrete task:** for each of the five candidate channels in `main.tex` Sec.~III, get an
order-of-magnitude comparison between the eHe platform's coherence-time-limited sensitivity and the
published exclusion curves of the corresponding dedicated experiment, before attempting any new QFI
derivation.
