---
name: two-qubit-gates
description: >-
  How high-fidelity two-qubit gates (√iSWAP and CZ) are designed and simulated for electrons on
  helium by time-dependent shaping of the double-well potential: the voltage functions V(λ(t)) and
  the erf-shaped ramp λ(t), the idle/entangling configurations, time propagation of the closed system
  (Crank–Nicolson) in a sinc-DVR product basis, average gate fidelity, grid-search optimization over
  ramp/hold times, ZZ suppression, gate-stability analysis, and the screening and ripplon-dephasing
  corrections. Use this skill whenever the user works on quantum gates, gate fidelity, √iSWAP or CZ or
  controlled-Z, pulse/ramp shaping, gate-time optimization, leakage/swap errors, ZZ coupling in a
  gate context, or gate robustness/decoherence for eHe (or analogous double-well) qubits. This is the
  gate-engineering layer (from the Phys. Rev. A 113, 032624 (2026) paper).
---

# Two-qubit gates with motional states of electrons on helium (Phys. Rev. A 113, 032624 (2026))

Gate-engineering layer. It sits on top of `coulomb-entanglement` (which provides the configurations
and eigenstates) and shares numerics with `ci-dvr-hartree-numerics`.

## Idea in one line

Drive the closed two-electron system from the **idle configuration I** into an **entangling
configuration (II for swap-type, III for CZ)** and back by making the gate voltages time-dependent,
`V(λ(t))`; the accumulated evolution, up to single-qubit `Z` rotations, realizes the target gate.

## Voltage functions and pulse shape

- Two voltage functions are studied:
  - `V^β(λ) = (1−λ)V^β_I + λV^β_III` — configurations optimized for **opposite-sign
    anharmonicities** `β_L = −β_R` (from the entanglement paper).
  - `V^ζ(λ) = (1−λ)V^ζ_I + λV^ζ_{II,III}` — configurations optimized to **directly minimize ZZ**
    coupling `ζ = E₄ − E₂ − E₁ + E₀`.
- The time dependence is an **error-function (smoothed top-hat) ramp**:

  ```
  λ(t) = (λ_max/2) [ erf((t − ½t_ramp)/(√2 σ)) − erf((t − t_gate + ½t_ramp)/(√2 σ)) ]
  ```

  with `t_gate = t_hold + 2 t_ramp`, `t_ramp = 4√2 σ`. Config I is at `λ=0`; the entangling config is
  held for `t_hold`. For `V^β`, `λ_max = λ_II ≈ 0.46` or `λ_III = 1` selects the gate; for `V^ζ`,
  `λ_max = 1` and the gate is chosen by using `V^ζ_II` or `V^ζ_III`. Entanglement is generated during
  the ramp *and* the hold when the transition is neither fully diabatic nor adiabatic — so the full
  time-dependent dynamics must be solved, not just endpoints.

## Simulating the dynamics

- Expand `|Ψ(t)⟩ = Σ_{αβ} C_{αβ}(t) |χ^L_α χ^R_β⟩` in **sinc-DVR** product functions (distinguishable
  particles; deep wells). Diagonal potential + closed-form kinetic and Coulomb matrix elements.
- Get the six lowest `t=0` eigenstates (`|00⟩,|01⟩,|10⟩,|02⟩,|11⟩,|20⟩`) with the **Davidson**
  method; propagate the four qubit states (`|00⟩,|01⟩,|10⟩,|11⟩` ≡ eigenstates 0,1,2,4) with the
  **Crank–Nicolson** propagator, step `Δt = (ω_qubit/2π)⁻¹/100 ≈ 0.001 ns` for `ω_qubit/2π ~ 10 GHz`.
- Build the `4×4` overlap matrix `U_{ij} = ⟨n_i | Ψ_{n_j}(t_gate)⟩` (omit the leaked `|02⟩`), apply
  single-qubit `R(θ_L,θ_R)=R_z(θ_L)⊗R_z(θ_R)`, giving `G = R U`.

## Figure of merit

Average gate fidelity (`d=4`):

```
F = [ Tr(M M†) + |Tr(M)|² ] / 20 ,   M = U₀† G(θ_L,θ_R)
```

with `U₀` the ideal target. Optimize `θ_L,θ_R` with a standard optimizer.

## Targets and best results

- **√iSWAP** (entangles `|01⟩↔|10⟩` into an equal superposition). A **swap error**
  `ε_swap = Σ|0.5 − |U_ij|²|/2` measures amplitude deviation — but note it is a *poor* fidelity
  predictor (relative phases matter more). Best: `F = 0.999` with `V^ζ` (t_ramp ≈ 1.41 ns, t_hold ≈
  0.1 ns → t_gate ≈ 2.9 ns); `V^β` reaches `F = 0.971`.
- **CZ** (π phase on `|11⟩`). A **leakage error** `ε_leak = 1 − |U₃₃|²` tracks CZ fidelity well. Best:
  `F = 0.996` for both voltage functions (`V^β`: t_gate ≈ 9.4 ns; `V^ζ`: ≈ 10.9 ns).
- Optimization is a **grid search** over (t_ramp, t_hold), warm-started across hold times for speed.

## Robustness (design takeaways)

- Fidelity oscillates with **ramp time**; for √iSWAP it is dominated by the phase accumulated during
  the ramp-up (large `|Ψ₁⟩–|Ψ₂⟩` energy difference), so it is **sensitive to ramp-time errors** and
  relatively stable to hold-time errors. Minimizing that ramp-up energy difference (e.g. by having
  the two states switch order between idle and entangling stages) improves stability.
- Direct **ZZ minimization (`V^ζ`)** yields the most stable gate (CZ with `V^ζ`: <1% fidelity change
  for ±0.1 ns deviations).

## Corrections beyond the closed, unscreened model

- **Screening.** Electrodes beneath the helium screen the Coulomb interaction (method of image
  charges: `u(r) = κ/r − κ/√(r²+(2h)²)`). Constant/first-order terms only shift energies and
  equilibria (reabsorbed by re-optimizing `V(λ)`); the **curvature term** `−u''(d)x₁x₂` is the
  entangling coupling. Screening factor `η = 1 − d³(d²−2h²)/(d²+4h²)^{5/2}`; for `d ≈ 1.5 µm`,
  `h = 500 nm`, `η ≈ 0.69` → gate time up ~`1/η ≈ 1.45×`. Moderate; high fidelities survive with
  retuning, and reduced coupling actually helps localize the useful voltage regions.
- **Decoherence.** The closed-system fidelities are upper bounds. In experiments, charge-qubit
  **dephasing** (~tens of MHz, e.g. ~60 MHz) is comparable to gate rates → must be suppressed.
  Proposed mechanisms: fluctuating background charges and **ripplon** coupling (tunable via pressing
  field `E⊥`; strong-coupling C≳1 gives ~100 MHz linewidth, weak-coupling reveals a narrow
  zero-ripplon line). High-fidelity operation favors the **low-pressing-field / weak-coupling**
  regime; a full treatment needs a Lindblad master equation.

## Guidance when using this skill

- Report gate time as `t_gate = t_hold + 2 t_ramp`, and state which voltage function (`V^β` vs `V^ζ`)
  and configuration were used — they change both fidelity and robustness.
- Keep the closed-system vs. open-system distinction explicit; label fidelities as closed-system
  upper bounds unless decoherence is modeled.
- Relative phases dominate √iSWAP fidelity; don't use amplitude-only errors as the objective.
- Numerics recipes → `ci-dvr-hartree-numerics`. Source:
  `papers/2026_Leinonen_two-qubit-gates_PRA113.pdf`, summary in
  `papers/summaries/two-qubit-gates.md`.
