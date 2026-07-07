# Summary — Sensing and Control of Single Trapped Electrons above 1 K

**Castoria, Beysengulov, Koolstra, Byeon, Glen, Sammon, Lyon, Pollanen, Rees** (2025). Phys. Rev. X
**15**, 041002. EeroQ Corporation. BibTeX key: `castoria2025`. PDF:
`../2025_Castoria_single-electron-sensing-above-1K_PRX15.pdf`.

## Thesis
Electrons on helium remain surface-bound up to several K (`Δ≈8 K` binding energy), so — unlike
standard mK cQED — their charge state can in principle be read out in cryostats with much higher
cooling power. This paper demonstrates, for the first time, **detection and deterministic
loading/unloading control of single trapped electrons at T = 1.1 K**, using a CPW resonator
dispersively coupled to an electrostatic trap that is physically separated from the electron reservoir.

## What they actually do
1. **Device.** Niobium microchannel reservoir (~40 channels) → single-channel link → electrostatic
   trap (split gate, unload gate, bottom electrode, resonator-bias electrode) → separately, a CPW
   resonator (`f_r=6.04383 GHz` bare) capacitively senses the trap. Reservoir is **not** coupled to the
   resonator (unlike earlier ensemble-coupled designs), isolating the readout from reservoir noise.
2. **Readout model.** Electric susceptibility `χ_e(ω)=Σ_n 4g_n²/(ω_n²−ω²+2iωΓ_n)` from the electron
   system's vibrational modes (found by energy minimization + Hamiltonian diagonalization for a given
   trap potential and `N_e`); dispersive shift `Δf≈−f_rRe[χ_e(2πf_r)]/2`.
3. **Bulk load/unload.** ~30-electron loading/unloading cycles via gate sweeps; `Δf` decreases on
   loading, increases on unloading, matching the model (`−14 kHz` calc vs `−17 kHz` observed).
4. **Single-electron isolation.** Reducing bias voltages reveals four discrete, irreversible `Δf`
   plateaus (`N_e=4,3,2,1`); max `|Δf|≈30 kHz` for `N_e=1` when trap curvature `ω_e` is tuned closest to
   `ω_r`. Single-electron coupling `g_e/2π=9.8 MHz` (2× prior eHe cQED work).
5. **Two-electron scaling.** In-phase mode couples as `g_{2+}=√2 g_e`, giving `Δf` twice the
   single-electron value — confirmed for single-well trap shapes, breaking down once the trap
   bifurcates into a double well.
6. **Reproducibility.** Repeated 1e/2e load–unload cycling (~22 kHz / ~44 kHz shifts) with **zero
   errors** over the measurement run.
7. **Validity at 1 K.** Plasma parameter `Γ_plasma=U_C/k_BT>30` (Coulomb energy dominates thermal
   energy); numerical search finds no metastable configurations for `N_e<8`; trap depth (~60 mV) vs
   `k_BT/e≈0.1 mV` gives a ~600× stability margin. Dominant relaxation channel: helium-vapor-atom
   scattering (`Γ_n/2π≈1–2 GHz` phenomenological fit), not ripplons (which dominate at mK).
8. **Sensitivity context.** Single-electron capacitance shift `δC_e≈0.45 aF`, between Rydberg
   image-charge detection (`~10⁻³ aF`) and semiconductor-QD rf reflectometry (`~1–10 aF`).

## Honest framing (carry into new work)
- This is **charge/orbital** detection and control — not spin readout. Spin-to-charge conversion
  remains a proposed, undemonstrated next step (as in `platform-electrons-on-helium`).
- A single dip (not two resonance crossings) is seen as the trap morphs from single- to double-well;
  the authors attribute this to a small residual field asymmetry keeping the system in the dispersive
  regime throughout — full resonance was not reached.
- Complements, but is a **different device and temperature regime** from, `resonator-coupling`
  (Koolstra et al.): that paper targets mK strong coupling for coherent control; this paper
  demonstrates >1 K robust counting/control for scalable loading.

## Related skills
`charge-readout` (primary), `resonator-coupling`, `platform-electrons-on-helium`,
`literature-and-notation`. Not to be confused with `quantum-sensing` (entangled-pair field/particle
metrology), which uses "sensing" in a different sense — see `charge-readout` for the disambiguation.
