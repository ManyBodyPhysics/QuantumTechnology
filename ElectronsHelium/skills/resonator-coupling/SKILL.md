---
name: resonator-coupling
description: >-
  Engineering the electron–photon coupling strength g for electrons on helium by designing
  high-impedance superconducting microwave resonators: the symmetrically coupled resonator (SCR)
  circuit (common/differential eigenmodes, dot capacitance, inductive-tail mode splitting),
  titanium-nitride (TiN) high-kinetic-inductance fabrication, the coupling formula
  g = ½eE_xω₀√(Z_res/m_eω_e), impedance/loss trade-offs (Q_i, Q_c, κ_i), and the roadmap from today's
  weak-coupling experiments to the strong-coupling regime. Use this skill whenever the user works on
  resonator design, circuit impedance engineering, electron–photon/charge–photon coupling strength,
  strong vs weak coupling for cQED with electrons on helium, TiN or kinetic-inductance resonators, SCR
  or common/differential mode circuits, or dispersive vs resonant electron-counting models built from
  a resonator Hamiltonian. This is the resonator hardware-design layer (from Koolstra et al., Phys.
  Rev. Appl. 23, 024001 (2025)) that the theory/gate/sensing skills assume as the physical readout.
---

# High-impedance resonators for strong coupling to an electron on helium (Phys. Rev. Appl. 23, 024001 (2025))

Hardware-design layer for the microwave side of the platform. It gives concrete circuit recipes for
turning the qualitative "readout via a microwave resonator" picture in `platform-electrons-on-helium`
into an engineered coupling strength `g`, and is the natural precursor to `charge-readout` (the
companion paper that uses a resonator to actually detect/count/control electrons). Device note: this
is a **separate experimental device (EeroQ Corporation collaboration)** from the Oslo 7-electrode
double-well device described in `literature-and-notation/references/notation.md` — don't merge their
geometries or symbols; treat this skill's numbers as belonging to their own hardware.

## The coupling formula and the strong-coupling target

```
g = ½ e E_x ω₀ √(Z_res / (m_e ω_e))
```

`E_x` = microwave electric field per volt at the electron, `ω₀` = resonator frequency, `ω_e` =
in-plane electron motional frequency, `Z_res` = resonator characteristic impedance. **Strong
coupling** means `g` exceeds both the photon loss rate `κ` and electron damping `Γ`. Baseline from
prior work: `g/2π ≈ 5 MHz` vs `Γ/2π ≈ 77 MHz` — deep in weak coupling; closing this gap needs roughly
an order-of-magnitude increase in `g`. Since `g ∝ √Z_res`, the lever is **resonator impedance**, not
just electric field or Q.

## Symmetrically coupled resonator (SCR) design

Two parallel LC resonators coupled through a dot capacitance `C_dot`, with the dot the only region
where the electron sits and interacts with the microwave field:

- **Differential mode** (co-rotating currents, purple in the paper's figures) — produces the
  microwave field `E_x` in the dot; this is the mode that couples to the electron.
- **Common mode** (counter-rotating currents) — no field at the dot center by symmetry; does *not*
  couple to a centered electron, but does allow a DC bias on the resonator center pin ("tail") without
  disturbing the differential mode. This decouples DC trap-tuning from the microwave design.
- Symmetric fully-degenerate circuit: `ω₀,c = 1/√(LC)`, `ω₀,d = 1/√(L(C+2C_x))`, `C_x = C_s + C_dot`.
- The **coupled (differential) design gives a √2 boost in g** over a single-ended scheme, because the
  voltage swing across `C_dot` is larger (both plates move).

### Lifting the common/differential degeneracy without losing impedance

Adding a small shunt `C_s` splits the modes but *lowers* `Z_res,d` — undesirable. Instead, add an
**inductive tail** `L_t` at the ground node between the two halves:

```
ω₀,c = 1/√(C(L+2L_t))        ω₀,d = 1/√(L(C+2C_x))        Z_res,d = √(L/(C+2C_x))
```

`Z_res,d` is **independent of `L_t`** — the tail is a free knob to split the modes (splitting
`∝ C_x/C − L_t/L`) with no impedance penalty. This is the key design trick to remember when asked
"how do you separate common and differential modes."

## Materials and fabrication

- **TiN (titanium nitride)** thin film: high kinetic sheet inductance `L□`, low microwave loss.
  Sheet inductance from `T_c` and sheet resistance: `L□ = ℏR□/(1.76π k_B T_c)`; measured
  `L□ = 178±13 pH/□`, `T_c = 2.80±0.05 K`, `R□ = 361±26 Ω/□` (ALD-grown, TiN(200) orientation
  favored — associated with lower loss than TiN(111)).
- No explicit capacitor — meandering wire capacitance to a far ground plane (`C ≈ 10 fF`) does the
  job; wire width `w = 1.6 µm` (optical-lithography compatible, comfortably above the superconducting
  coherence length to suppress phase-slip loss). Footprint `< 250 × 180 µm²`.
- **Measured performance** (18 resonances, two device variants A/B, 3–6 GHz): median internal
  quality factor `Q_i = 3.9×10⁵`, average impedance `≈ 2.5 kΩ`, internal loss rate
  `κ_i/2π = 11.7 kHz`. → a **sevenfold** predicted boost in `g` vs a standard 50 Ω resonator
  (`√(2500/50) ≈ 7`), since a mock electrode/airbridge for future electron trapping does not degrade
  `Q_i`.
- Impedance scales with geometry as `Z_res,d ∝ (ℓ/w³)^{1/4}`, `f₀ ∝ (w/ℓ³)^{1/4}` (ℓ = meander
  length). Narrowing `w` (e.g. ×8, needs e-beam lithography) while halving `ℓ` projects `Z ≈ 10 kΩ`
  (≈14× vs 50 Ω), approaching or exceeding the resistance quantum `R_Q ≈ 6.45 kΩ`.

## Modeling and simulation results

- Circuit model verified against 18 measured resonances: capacitance matrix from FEM, inductance from
  `L = L□ ℓ/w`, with a single fit discount factor `γ ≈ 0.61` (bounded `(2/π)² ≤ γ ≤ 1`) correcting for
  the distributed (non-lumped) nature of the meandering-wire mode — gives `<2%` frequency error across
  all resonators.
- **Dispersive electron counting**: simulated frequency shifts for `n = 0,1,2` electrons are
  `~0.1 MHz`, resolvable against `<1 MHz` linewidths — sufficient to count a few electrons
  off-resonance even when detuned by several GHz.
- **Resonant regime**: for one electron tuned onto resonance (`ω_dot = ω₀,d`), simulations show a
  `2g` avoided crossing between electron motion and the differential mode; for a realistic
  `E_x = 0.25 µm⁻¹`, `g/2π = 43 MHz` — approaching strong coupling. The common mode stays uncoupled,
  confirming only the differential mode matters for electron readout.

## What this buys, and what's still open

- Practical near-term projection: `g/2π ≈ 80 MHz` with a narrower/shorter resonator — comparable to
  typical superconducting-qubit coupling strengths.
- **Not yet demonstrated in this paper**: coupling to an actual trapped electron (helium
  microchannels + trapping/tuning electrodes are future work); biasing the tail with a real DC
  electrode (rather than shorting it to ground) is expected to damp the common mode resistively and
  makes `Q_i` sensitive to capacitive asymmetry — a **1% asymmetry** is estimated to drop `Q_i` below
  `10⁵`.
- Complementary companion result: `charge-readout` (Castoria et al.) demonstrates actual single- and
  few-electron loading/counting/control using a (different, CPW-based) resonator design, at
  temperatures above 1 K rather than the ~10 mK dilution-fridge regime used here.

## Guidance when using this skill

- Keep the **strong-coupling condition** (`g > κ, Γ`) and the current numeric gap (order of magnitude
  needed) explicit; don't imply strong coupling has been achieved — it is a design/roadmap result.
- Distinguish **measured** device properties (`Q_i`, `Z_res ≈ 2.5 kΩ`, `κ_i/2π = 11.7 kHz`) from
  **simulated/projected** ones (electron coupling `g/2π = 43 MHz`, the 14× narrow-wire projection,
  `g/2π ≈ 80 MHz`).
- Don't conflate this device's geometry/units with the Oslo 7-electrode double-well device in
  `literature-and-notation` — they are different hardware from different (though overlapping-author)
  efforts.
- Source: `papers/2025_Koolstra_high-impedance-resonators_PRApplied23.pdf`, summary in
  `papers/summaries/high-impedance-resonators.md`. BibTeX key: `koolstra2025impedance`.
