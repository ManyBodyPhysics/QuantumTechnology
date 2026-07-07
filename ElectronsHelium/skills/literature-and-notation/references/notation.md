# Notation, units, and constants

Shared conventions across the electrons-on-helium project. Match these exactly in new work.

## Unit systems

- **Primary natural units:** `ℏ²/2mₑ = 1` and `ℏ = 1` (⇒ `mₑ = ½`). Consequences: energy ~ 1/length²,
  so **time has units of `µm²`** in the sensing/gate dynamics. Always state this and give at least one
  conversion to SI (e.g. express a representative `δB` in tesla and an interrogation time in ns).
- **Device energy unit:** `E_d = ℏ²/(mₑ x₀²)` with length unit `x₀ = 123 nm` (characteristic
  interelectron distance at ~2×10⁹ cm⁻² density). Transition frequencies are quoted in GHz.

## Constants and standard values

| Symbol | Meaning | Value / convention |
|---|---|---|
| `κ` | soft-Coulomb strength | `2326` (in `E_d`) |
| `ε` | Coulomb regularizer | `1e-2` |
| `x₀` | length unit | `123 nm` |
| `d` | electron separation | `≈ 1.5 µm` |
| `h` | helium depth (screening) | `500 nm` |
| electrodes | count / width / pitch | 7 / 200 nm / 200 nm |
| `N_x=N_y` | reference 2D grid | `20` (400 points) |
| level spacing | in-plane `x` | `5–15 GHz` |
| `y` stiffness | vs `x` | ~6× higher frequency |

## Symbols

- `v(x) = −Σ_k α_k(x) V_k` — trap potential from electrode voltages `V_k`; `α_k` electrode form
  factors (FEM).
- `u(x₁,x₂) = κ/√((x₁−x₂)²+ε²)` — soft Coulomb.
- `ψ_k, ε_k` — single-particle eigenstates/energies; `φ^A_i` — Hartree/localized orbitals in well
  `A ∈ {L,R}`; `L0,L1,…,R0,R1,…` — energy-ordered localized orbitals.
- `|Ψ_n⟩ = Σ_{ij} C_{ij,n} |φ^L_i φ^R_j⟩`, energy `E_n`; `S_n` — von Neumann entropy (base-2).
- Configurations **I / II / III**; interpolation `V(λ) = (1−λ)V_I + λV_III`.
- `ω_A` transition frequency, `β_A` anharmonicity (convention `β_L = −β_R = Δ_I/2`), detuning
  `Δ ≡ ω_L − ω_R`.
- ZZ coupling `ζ = E₄ − E₂ − E₁ + E₀`.
- Gate pulse: `λ(t)` erf-ramp, `t_ramp`, `t_hold`, `t_gate = t_hold + 2 t_ramp`, `λ_max`
  (`λ_II ≈ 0.46`, `λ_III = 1`); voltage functions `V^β`, `V^ζ`.
- Gate matrices `U` (raw overlap), `G = R(θ_L,θ_R)U`; fidelity `F = [Tr(MM†)+|Tr M|²]/20`,
  `M = U₀†G`. Errors: swap `ε_swap`, leakage `ε_leak = 1−|U₃₃|²`.
- Sensing: local fields `B_L,B_R`; `B̄=(B_L+B_R)/2`, `δB=B_L−B_R`; spin ops `S^z_{L,R}`;
  `H_B = gµ_B(B_L S^z_L + B_R S^z_R)`; reference states `|S*⟩,|T₀*⟩`; effective coupling
  `λ(δB) = (gµ_B δB/2) M_ge`, `M_ge = ⟨e|S^z_L−S^z_R|g⟩`, splitting `Δ_ST = E_e−E_g`.
- Fisher information `F_Q` (quantum), `F_C` (classical), `F_C ≤ F_Q`; Cramér–Rao
  `Var(ϕ_est) ≥ 1/(ν F_Q)`.

## Resonator / readout hardware (separate EeroQ device family — `koolstra2025impedance`, `castoria2025`)

These two papers describe **real, fabricated devices from the EeroQ Corporation collaboration** —
different specific hardware from the Oslo 7-electrode double well above, even though authorship
overlaps (Beysengulov, Pollanen). Do not merge geometries, electrode counts, or length scales between
the two families; do cite both when discussing how a proposal's readout step would actually be built.

- Coupling strength `g = ½eE_xω₀√(Z_res/(m_eω_e))`; strong coupling requires `g > κ, Γ` (`κ` = photon
  loss rate, `Γ` = electron damping — note `κ` here is a *loss rate*, unrelated to the soft-Coulomb
  `κ=2326` above; disambiguate by context).
- Resonator eigenmodes: common (`ω₀,c`) and differential (`ω₀,d`); dot capacitance `C_dot`, shunt
  `C_s`, `C_x=C_s+C_dot`; tail inductance `L_t`; characteristic impedance `Z_res,d=√(L/(C+2C_x))`.
- Quality factors `Q_i` (internal), `Q_c` (coupling); loss rate `κ_i=ω₀/Q_i`.
- Electric susceptibility `χ_e(ω)=Σ_n4g_n²/(ω_n²−ω²+2iωΓ_n)`; dispersive frequency shift
  `Δf≈−f_rRe[χ_e(2πf_r)]/2`; single-electron coupling `g_e`, two-electron in-phase coupling
  `g_{2+}=√2g_e`.
- Representative measured/simulated values (`koolstra2025impedance`): `Z_res≈2.5 kΩ`,
  `Q_i=3.9×10⁵`, `κ_i/2π=11.7 kHz`, `g/2π=43 MHz` (simulated, on resonance). (`castoria2025`):
  `f_r=6.04383 GHz`, `g_e/2π=9.8 MHz`, `T=1.1 K`.

## Sign / structure conventions to preserve

- `(S^z_L − S^z_R)|S⟩ = |T₀⟩` and `(S^z_L − S^z_R)|T₀⟩ = |S⟩`; uniform field does not mix S and T₀.
- Detunings in configuration I and III have **opposite sign** by design (guarantees config II on the
  interpolation path).
- Use `⊗` (tensor product) for combining qubit states, e.g. `|0⟩_L ⊗ |0⟩_R = |00⟩` (not `⊕`).
- Entanglement entropy uses **base-2 log**.

## Claims discipline

- Mark spin-coherence times and network `1/N` scaling as **predicted / proposed**, not demonstrated.
- The two-electron QFI advantage is a **factor of 2** (N=2 Heisenberg), reduced by `|M_ge|²` and
  finite detuning in the full CI.
- Distinguish **closed-system** gate fidelities (upper bounds) from open-system estimates.
- `koolstra2025impedance`: resonator fabrication/`Q_i`/`Z_res`/circuit-model accuracy are
  **demonstrated**; coupling to an actual trapped electron (`g/2π=43 MHz`, the narrow-wire
  `g/2π≈80 MHz` projection) is **simulated/projected**, not measured.
- `castoria2025`: charge/orbital sensing and single-electron control at `T=1.1 K` are **demonstrated**;
  spin readout is still **not demonstrated** on this or any eHe device — only proposed via
  spin-to-charge conversion.
