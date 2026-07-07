---
name: quantum-sensing
description: >-
  The entanglement-enhanced quantum-sensing framework for electrons on helium: using an entangled
  two-electron singlet as a differential sensor, encoding a signal (e.g. a magnetic-field gradient
  δB) by coherent singlet–triplet mixing, and quantifying the attainable precision with the quantum
  Fisher information (QFI), classical Fisher information (CFI), and the quantum Cramér–Rao bound, plus
  the independent-spin (Ramsey) benchmark, the standard-quantum-limit vs Heisenberg (1/√N vs 1/N)
  scaling, reinforcement-learning optimization of the trap, and extension to correlated sensor
  networks. Use this skill whenever the user works on quantum sensing, metrology, Fisher information,
  Cramér–Rao bounds, singlet–triplet sensing, differential/common-mode field detection, dark-matter
  or axion sensing concepts, sensor networks, or the DRD5 sensor proposal on the eHe platform. This
  is the sensing layer (from the 2026 Perruzza et al. quantum-sensing manuscript).
---

# Entanglement-enhanced quantum sensing with electrons on helium (Perruzza et al., 2026)

Sensing layer. It reuses the entangled states from `coulomb-entanglement` and the trap/pulse control
from `two-qubit-gates`, and adds parameter-estimation theory. Numerics (Fisher information,
propagation, RL) → `ci-dvr-hartree-numerics`.

## Core idea: the singlet as a differential sensor

Two spins prepared in the entangled singlet `|S⟩=(|↑↓⟩−|↓↑⟩)/√2` (total spin 0) are **insensitive to
uniform, common-mode fields** but **maximally sensitive to a difference** between the two sites. A
local perturbation (a passing particle, a transient field) that differs between the two wells drives
`|S⟩ ↔ |T₀⟩`, giving a measurable phase / population change while common-mode backgrounds
(uniform fields, vibrations) cancel. This is the metrological reason to entangle.

## Signal encoding (magnetic-field gradient)

Zeeman coupling with local fields `B_L,B_R`, `B̄=(B_L+B_R)/2`, `δB=B_L−B_R`:

```
H_B = gµ_B(B_L S^z_L + B_R S^z_R)
    = gµ_B B̄ (S^z_L+S^z_R)  +  (gµ_B δB/2)(S^z_L−S^z_R)
```

The uniform term does **not** mix `|S⟩,|T₀⟩`; the **gradient term does**, with
`⟨T₀|H_B|S⟩ = gµ_B δB/2` (because `(S^z_L−S^z_R)|S⟩=|T₀⟩`). In the full CI states the relevant
ground `|g⟩` (singlet-like) and excited `|e⟩` (triplet-like) give an effective two-level model:

```
H_eff = E_g|g⟩⟨g| + E_e|e⟩⟨e| + λ(δB)(|g⟩⟨e|+|e⟩⟨g|),
λ(δB) = (gµ_B δB/2) M_ge ,  M_ge = ⟨e|S^z_L−S^z_R|g⟩,  Δ_ST = E_e−E_g.
```

`M_ge = 1` for an ideal isolated L0–R0 pair; deviations quantify charge admixture / leakage.
Prepared in `|g⟩`, the signal appears as coherent oscillation into `|e⟩`:

```
P_{g→e}(t) = [4λ²/(Δ_ST²+4λ²)] sin²( (t/2ℏ)√(Δ_ST²+4λ²) ).
```

## Precision: Fisher information & Cramér–Rao

For `ν` repetitions and unbiased estimator of `ϕ`:

```
Var(ϕ_est) ≥ 1/(ν F_Q(ϕ))          (quantum Cramér–Rao bound)
F_Q = 4[⟨∂ϕψ|∂ϕψ⟩ − |⟨ψ|∂ϕψ⟩|²]    (pure state)
F_C = Σ_m (∂ϕ p_m)²/p_m ≤ F_Q       (specific measurement)
```

Set `ϕ ≡ δB`. The binary singlet–triplet readout `{|e⟩⟨e|, 1−|e⟩⟨e|}` gives a `F_C` that oscillates
and **dips** where `∂_{δB}P_{g→e}=0` (readout locally insensitive) — a signature feature. The QFI of
the effective dynamics:

```
F_Q^{ST}(t) = [4(gµ_B)² |M_ge|² / Δ_ST²] sin²(Δ_ST t / 2ℏ)
            ≃ |M_ge|² (gµ_B t/ℏ)²   for Δ_ST t/ℏ ≪ 1.
```

## The benchmark and the (modest, honest) gain

Independent-spin **Ramsey** benchmark (two separable equatorial spins, generator
`G_{δB}=(gµ_B t/2ℏ)(S^z_L−S^z_R)`, `Var(S^z_L−S^z_R)=1/2`):

```
F_Q^{ind}(t) = ½ (gµ_B t/ℏ)² .
```

For an ideal pair `M_ge=1`, `F_Q^{ST} = 2 F_Q^{ind}` — a **factor-of-2** QFI gain. Frame this
correctly: it is the **N=2 instance of Heisenberg scaling** (`F_Q ∝ N²` vs SQL `F_Q ∝ N`), not a
demonstrated `1/N` scaling. In the full CI it is reduced by `|M_ge|²` and finite-detuning effects
(numerically the relative difference from ×2 is <1% at optimum). Do **not** oversell: the two-electron
result is a fixed factor; the `1/N` network scaling below is a proposal.

## Optimizing the probe (reinforcement learning)

The double-well shape is optimized by **RL (Actor–Critic, PPO)** over the electrode voltages to
**maximize a Fisher-information-based reward**. Reward (schematically):

```
R(a) = r_f · r_cfi − (ω_µ p_µ + ω_b p_b),
r_f = F_singlet · F_triplet,   r_cfi = cfi₃ + α·cfi₂,
```

combining singlet/triplet state fidelities with the two-channel (binary) and three-channel
(spin-resolved) classical FI, penalizing delocalized orbitals `p_µ` and low central barrier `p_b`.
One-shot episodes; hyperparameters live in the paper's Table 1. See `ci-dvr-hartree-numerics` for the
reward/FI computation and RL scaffolding.

## From two qubits to sensor networks (proposal, not yet demonstrated)

Extending interaction-mediated entanglement to an **array** with engineered neighbour couplings
prepares a many-body entangled state whose collective response to a *localized* perturbation is
enhanced; a local event imprints a correlated signature read out through joint observables. Two
complementary resources on one platform:

- **Singlet** → optimal for **field gradients** (generator `G₋`), immune to common-mode drift.
- **Bell/GHZ-type** → optimal for **common-mode** fields (generator `G₊`).

Each reaches Heisenberg scaling `F_Q ∝ N²` for its generator; the unifying quantity is the QFI and the
unifying resource is the **variance of the field-coupling generator** in the entangled probe.

## Target signals (framing)

Sub-eV energy deposition from light dark matter; single-electron/Rydberg excitations; weak, slowly
oscillating fields from ultralight dark matter / axions (effective time-dependent Zeeman shifts).
Entangled sensor networks have been proposed for dark-matter/axion searches. Keep these as
*motivating targets*, and keep time-dependent-field sensing flagged as future work (the paper treats
the static-gradient case).

## Guidance when using this skill

- Distinguish QFI (best over all measurements) from CFI (a specific readout); report the CRB.
- State the factor-of-2 result as N=2 Heisenberg, not a scaling demonstration; mark network `1/N` as
  aspirational.
- Keep `M_ge`, `Δ_ST`, `λ(δB)` definitions consistent with `coulomb-entanglement`.
- Natural units throughout; give a physical-unit conversion for `δB` (T) and `t` (ns). See
  `literature-and-notation`. Source: `papers/2026_Perruzza_quantum-sensing-eoh.pdf`, summary in
  `papers/summaries/quantum-sensing.md`.
- If asked how the singlet–triplet readout would actually be implemented in hardware, point to
  `resonator-coupling` (coupling-strength engineering) and `charge-readout` (demonstrated dispersive
  electron detection) — but note these two demonstrate **charge/orbital** sensing on a different
  device; the spin-to-charge conversion step this skill's readout assumes is still not demonstrated
  anywhere on this platform. Don't conflate this skill's "sensing" (entangled-pair field/particle
  metrology) with `charge-readout`'s "sensing" (electron/charge detection).
