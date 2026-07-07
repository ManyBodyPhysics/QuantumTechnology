# Summary — Design and dynamics of two-qubit gates with motional states of electrons on helium

**Leinonen, Flaten, Bilek, Schøyen, Hjorth-Jensen, Beysengulov, Stewart, Weidman, Wilson.**
Phys. Rev. A **113**, 032624 (2026). BibTeX key: `leinonen2025`.
PDF: `../2026_Leinonen_two-qubit-gates_PRA113.pdf`.

## Thesis
Show, by exact closed-system time evolution, that **high-fidelity two-qubit gates** (`√iSWAP`, `CZ`)
are achievable for motional (charge) states of two electrons on helium by **time-dependent shaping of
the double-well potential**, and characterize their stability, then discuss screening and decoherence.

## Method
- Build on the entanglement paper's configurations. Two voltage functions:
  `V^β` (opposite-sign anharmonicities `β_L=−β_R`) and `V^ζ` (direct **ZZ minimization**,
  `ζ = E₄−E₂−E₁+E₀`).
- **Erf ramp** `λ(t) = (λ_max/2)[erf((t−½t_ramp)/√2σ) − erf((t−t_gate+½t_ramp)/√2σ)]`,
  `t_gate = t_hold + 2 t_ramp`, `t_ramp = 4√2σ`. Idle config at `λ=0`; entangling config held for
  `t_hold`. Entanglement is generated during both ramp and hold (intermediate diabatic/adiabatic).
- **Distinguishable-particle** sinc-DVR product basis; six lowest `t=0` eigenstates via **Davidson**;
  propagate the four qubit states with **Crank–Nicolson** (`Δt ≈ 0.001 ns`). Build `U_{ij}` overlaps,
  apply single-qubit `Z` rotations `G = R U`.
- **Average gate fidelity** `F = [Tr(MM†)+|Tr M|²]/20`, `M = U₀†G`; optimize `θ_L,θ_R`.

## Results
- **√iSWAP:** swap error `ε_swap` is a *poor* fidelity predictor (relative phases dominate). Best
  `F = 0.999` with `V^ζ` (t_ramp≈1.41, t_hold≈0.1 → **t_gate≈2.9 ns**); `V^β` reaches `F = 0.971`.
- **CZ:** leakage error `ε_leak = 1−|U₃₃|²` tracks fidelity well. Best `F = 0.996` for both functions
  (`V^β`: **t_gate≈9.4 ns**; `V^ζ`: ≈10.9 ns).
- Optimization by **grid search** over (t_ramp, t_hold), warm-started across hold times.
- **Stability:** fidelity oscillates with ramp time; √iSWAP is sensitive to ramp-time deviations
  (phase accumulated during ramp-up, where the `|Ψ₁⟩–|Ψ₂⟩` energy difference is large) and stable to
  hold-time deviations. Direct ZZ minimization (`V^ζ`) gives the most stable gate (CZ: <1% change for
  ±0.1 ns deviations). Design lesson: make `|Ψ₁⟩`,`|Ψ₂⟩` switch order between idle and entangling
  stages to reduce the ramp-up energy difference.

## Beyond the closed, unscreened model
- **Screening** (image charges): `u(r)=κ/r − κ/√(r²+(2h)²)`. Only the **curvature** term
  `−u''(d)x₁x₂` entangles; screening factor `η = 1 − d³(d²−2h²)/(d²+4h²)^{5/2}`; for `d≈1.5 µm`,
  `h=500 nm`, `η≈0.69` → gate time ×~`1/η≈1.45`. High fidelities survive with retuning; reduced
  coupling helps localize useful voltage regions.
- **Decoherence:** closed-system fidelities are upper bounds. Charge dephasing ~**60 MHz** is
  comparable to gate rates; mechanisms are fluctuating background charges and **ripplon** coupling
  (tunable via pressing field `E⊥`; strong-coupling ~100 MHz linewidth; weak-coupling reveals a narrow
  zero-ripplon line). Favor low-pressing-field/weak-coupling operation; full treatment needs a
  Lindblad master equation. Appendices derive screening and the electron–ripplon Hamiltonian.

## Related skills
`two-qubit-gates` (primary), `coulomb-entanglement`, `ci-dvr-hartree-numerics`,
`platform-electrons-on-helium`.
