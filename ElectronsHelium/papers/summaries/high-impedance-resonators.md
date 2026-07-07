# Summary — High-Impedance Resonators for Strong Coupling to an Electron on Helium

**Koolstra, Glen, Beysengulov, Byeon, Castoria, Sammon, Dizdar, Wang, Schuster, Lyon, Pollanen, Rees**
(2025). Phys. Rev. Appl. **23**, 024001. EeroQ Corporation / University of Chicago / Stanford.
BibTeX key: `koolstra2025impedance`. PDF: `../2025_Koolstra_high-impedance-resonators_PRApplied23.pdf`.

## Thesis
Reaching **strong coupling** between a microwave photon and an electron's in-plane motion on helium
requires roughly an order-of-magnitude increase in coupling strength `g` over prior work
(`g/2π≈5 MHz` vs damping `Γ/2π≈77 MHz`). Since `g ∝ √Z_res`, the fix is a **high-impedance
resonator**. The paper designs, fabricates, and characterizes such a resonator (without yet coupling
it to a trapped electron) and validates a circuit model that predicts its properties.

## What they actually do
1. **Circuit design.** A symmetrically coupled resonator (SCR): two LC halves coupled through a dot
   capacitance `C_dot`, with common and differential eigenmodes. Only the differential mode produces a
   field at the dot; the design gives a √2 coupling boost over single-ended schemes and allows a DC
   bias ("tail") that doesn't perturb the microwave mode.
2. **Mode-splitting trick.** An inductive tail `L_t` splits common/differential frequencies
   (`ω₀,c=1/√(C(L+2L_t))`, `ω₀,d=1/√(L(C+2C_x))`) while leaving `Z_res,d=√(L/(C+2C_x))` **unchanged** —
   avoids the usual impedance penalty of shunt-capacitance-based splitting.
3. **Fabrication.** TiN (titanium nitride) meandering-wire resonators (no explicit capacitor), ALD-grown
   on Si(100), `w=1.6 µm`, footprint `<250×180 µm²`; sheet inductance `L□=178±13 pH/□` from
   `T_c=2.80±0.05 K`, `R□=361±26 Ω/□`.
4. **Measurement.** 18 resonances (2 device variants, one with a mock trapping electrode/airbridge):
   median `Q_i=3.9×10⁵`, average `Z_res≈2.5 kΩ`, `κ_i/2π=11.7 kHz` — implying a **sevenfold** coupling
   boost vs 50 Ω resonators; mock electrode does not degrade `Q_i`.
5. **Model verification.** Capacitance-matrix FEM + measured sheet inductance, with a single
   distributed-capacitance discount factor `γ=0.61±0.01`, predicts all 18 eigenfrequencies to `<2%`.
6. **Simulated electron coupling** (not yet measured with a real electron): dispersive counting
   resolves `n=0,1,2` electrons (`~0.1 MHz` shifts); on resonance, a `2g` avoided crossing gives
   `g/2π=43 MHz` for a realistic field `E_x=0.25 µm⁻¹`.

## Honest framing (carry into new work)
- **Demonstrated**: resonator fabrication, TiN material properties, `Q_i`, `Z_res`, circuit-model
  accuracy. **Not yet demonstrated**: coupling to an actual trapped electron (needs helium
  microchannels + trap electrodes — flagged as ongoing work) and DC-biased tail operation (electrode
  asymmetry is estimated to limit `Q_i`, not yet tested).
- The `g/2π=43 MHz` and further `g/2π≈80 MHz` (narrower-wire) numbers are **projections/simulations**,
  not measurements.
- This is a hardware/design paper; pair with `charge-readout` (Castoria et al.) for a paper that
  actually detects and controls electrons with a resonator, albeit a different CPW-based design and a
  very different temperature regime (>1 K vs the ~10 mK used here).

## Related skills
`resonator-coupling` (primary), `charge-readout`, `platform-electrons-on-helium`,
`literature-and-notation`.
