---
name: charge-readout
description: >-
  Dispersive microwave-resonator charge sensing and deterministic loading/unloading control of single
  and few trapped electrons on helium, demonstrated at temperatures above 1 K: the electric
  susceptibility model χ_e(ω) of electron vibrational modes, the resonator frequency shift
  Δf ≈ −f_r Re[χ_e(2πf_r)]/2, single- and two-electron coupling strengths (g_e, g_{2+}=√2 g_e), the
  classical-electron / finite-temperature validity regime (k_BT > ℏω_e, plasma parameter Γ_plasma),
  electron counting via discrete Δf plateaus, and metastable-configuration checks. Use this skill
  whenever the user works on charge sensing, electron counting, dispersive readout, single-electron
  loading/unloading control, trap curvature tuning, resonator frequency-shift models, single-electron
  capacitance, or experiments/proposals operating above the usual ~10-100 mK cQED regime. This is the
  demonstrated charge-detection layer (from Castoria et al., Phys. Rev. X 15, 041002 (2025)).
---

# Sensing and control of single trapped electrons above 1 K (Phys. Rev. X 15, 041002 (2025))

Demonstrated charge-readout layer. It shows what a resonator-coupled electron trap can actually do —
count and deterministically control single electrons — using a CPW resonator design distinct from the
SCR of `resonator-coupling`, and operating far above typical dilution-fridge cQED temperatures. Device
note: this is the **same EeroQ-collaboration hardware family as `resonator-coupling`** but a different
specific device (CPW split-ring resonator + separate reservoir/trap microchannels), and again distinct
from the Oslo 7-electrode device in `literature-and-notation`.

## Why operate above 1 K

Standard dilution-refrigerator cQED offers only ~1 mW cooling power at 100 mK, a scaling bottleneck
for large qubit arrays. Electrons on helium stay bound to the surface up to several K (binding energy
`Δ ≈ 8 K`), so they can in principle be read out in pumped ⁴He cryostats with >100 mW cooling power —
the same appeal that has driven Si spin-qubit operation above 1 K. This paper is the first
demonstration that single-electron detection/control survives at these elevated temperatures
(`T = 1.1 K` here), where `k_BT` exceeds the electron motional energy `ℏω_e` by several times and
⁴He vapor pressure is non-negligible — a regime qualitatively different from mK cQED.

## Device concept

- Niobium microchannel network: a ~40-channel electron **reservoir** connected by a single narrow
  channel to an electrostatically defined **trap**, itself capacitively coupled to (but physically
  separate from) a CPW **resonator** electrode (bare differential-mode `f_r = 6.04383 GHz`).
- Electrodes: split gate `V_sg` (barrier to the reservoir), unload gate `V_un`, resonator bias `V_r`
  (also sets trap curvature), bottom electrode `V_b` (attractive base potential).
- Key architectural advantage over earlier devices: **the reservoir is not coupled to the resonator**
  — only trapped electrons shift the resonance, so the readout is insensitive to reservoir electron
  number/noise. (Contrast with the earlier ensemble-coupled design in `koolstraCouplingSingleElectron2019`.)

## The dispersive charge-sensing model

Trapped electrons act as polarizable matter inside the cavity with electric susceptibility

```
χ_e(ω) = Σ_n 4g_n² / (ω_n² − ω² + 2iωΓ_n)
```

summing Lorentzian responses of the electron system's vibrational (collective motional) modes:
`ω_n` = mode eigenfrequency, `Γ_n` = phenomenological damping, `g_n` = coupling of that mode to the
microwave field (built from FEM lever-arm functions `α^{a,b}(x,y)` and the mode eigenvector). In the
weak-coupling (dispersive) limit:

```
Δf ≈ −f_r Re[χ_e(2πf_r)] / 2
```

Workflow to predict `Δf` for `N_e` electrons in a given trap potential: (1) minimize the classical
Coulomb + confinement energy for the equilibrium electron configuration, (2) diagonalize the resulting
vibrational-mode Hamiltonian for `{ω_n}` and eigenvectors, (3) project the resonator field onto each
mode to get `g_n`, (4) evaluate `χ_e` and `Δf`.

## Single- and few-electron results

- **Single electron**: coupling `g_e/2π = 9.8 MHz` (2× the coupling reported in earlier eHe cQED work,
  `koolstraCouplingSingleElectron2019`). `Δf` is maximized (`~30 kHz` observed) when the trap curvature
  `ω_e` is tuned closest to `ω_r`; the sign/shape of the dip is reproduced by the model using FEM trap
  potentials.
- **Two electrons**: the in-phase (center-of-mass) motional mode couples as `g_{2+} = √2 g_e` (same
  frequency as the single-electron mode in the harmonic approximation), giving `Δf` twice as large as
  the single-electron case — but only while the trap remains a single well; once it splits into a
  double well the factor of 2 breaks down (out-of-phase motion instead couples to the *common* mode,
  which is off-resonance here).
- **Counting**: sweeping the unload gate produces discrete, irreversible `Δf` **plateaus** as electrons
  leave one at a time — `N_e = 4,3,2,1,0` resolved. Repeated single-/double-electron load–unload
  cycling (~22 kHz / ~44 kHz shifts) showed **no errors**, i.e. reproducible deterministic control.
- Single-electron effective capacitance shift `δC_e ≈ 0.45 aF` (quantum-capacitance-like), roughly
  comparable to semiconductor-QD rf-reflectometry sensitivities (`δC_e ~ 1–10 aF`) and much larger than
  out-of-plane Rydberg image-charge detection (`δC_e ~ 10⁻³ aF`).

## Why it still works at 1 K: validity checks

- **Plasma parameter** `Γ_plasma = U_C/k_BT > 30` under the experimental conditions — Coulomb energy
  dominates thermal energy, so the electron configuration stays in its classical ground state (thermal
  fluctuations don't scramble it).
- **Metastable configurations**: numerical search (gradient descent + annealing off) finds no
  metastable states for `N_e < 8` under the trap geometries used; for larger `N_e`, Coulomb repulsion
  drives zigzag configurations with accessible low-lying metastable states — flag this if extending to
  larger electron numbers.
- **Trap depth vs thermal energy**: potential well ~60 mV deep vs `k_BT/e ≈ 0.1 mV` — a ~600× margin
  explains the observed reliability of single-electron confinement despite `T = 1.1 K`.
- Dominant relaxation channel at these temperatures is **helium-vapor-atom scattering** (not ripplons,
  which dominate at mK); phenomenological `Γ_n/2π ≈ 1–2 GHz` fits the data better than smaller values.

## Relationship to the rest of the project

- This is a **charge/orbital** readout, not spin readout — spin-to-charge conversion (as invoked in
  `platform-electrons-on-helium` and `quantum-sensing`) is still required and not demonstrated here.
- Complements `resonator-coupling`: that paper pushes toward **strong coupling** at ~10 mK for
  coherent gates; this paper demonstrates **robust electron counting/control** at >1 K for scalable
  loading — two different points on the temperature/coupling design space, both relevant when framing
  a scaling roadmap.
- Don't confuse this paper's "sensing" (charge/electron-number detection, an engineering readout tool)
  with the `quantum-sensing` skill's "sensing" (entangled-pair field/particle metrology for HEP) — they
  use the word differently. If both come up, say so explicitly to avoid ambiguity.

## Guidance when using this skill

- State `Δf` results with the sign convention used in the paper (electrons **decrease** `f`, i.e.
  `Δf < 0`), and note whether a value is measured or computed from `χ_e(ω)`.
- Keep the **T = 1.1 K** operating point and the classical/thermal validity argument (`Γ_plasma`,
  metastability check) explicit — it's the paper's central claim, not an incidental detail.
- Distinguish demonstrated **charge/orbital** control from **not-yet-demonstrated spin** readout.
- Source: `papers/2025_Castoria_single-electron-sensing-above-1K_PRX15.pdf`, summary in
  `papers/summaries/single-electron-sensing-above-1K.md`. BibTeX key: `castoria2025`.
