# Summary — Electrons on Helium and Entangled Quantum Sensors for Particle Physics

**Perruzza, Beysengulov, Bilek, Camper, Flaten, Hjorth-Jensen, Lange, Leinonen, Malamant, Massel,
Pollanen, Sandaker, Stewart, Svensson, Weidman** (2026). Associated with the CERN DRD5 collaboration.
BibTeX key: `perruzza2026`. PDF: `../2026_Perruzza_quantum-sensing-eoh.pdf`.

## Thesis
Propose a quantum sensor for particle physics built from an **entangled pair of electron qubits on
superfluid helium**. An entangled singlet is a **differential** sensor — blind to common-mode fields,
maximally sensitive to differences between the two sites — so it can pick up tiny, localized signals
below conventional detector thresholds. Framed within CERN's DRD5 (RD-quantum) program.

## What they actually compute
1. **Device & orbitals.** A double-well trap (RL-optimized voltages) on helium; single-particle
   spectrum on a 2D sine-DVR grid; localized orbitals via a spatial projection operator (left/right
   labels L0,L1,…/R0,R1,…).
2. **Two-electron CI.** Configuration-interaction two-electron states; identify the maximally
   entangled (1,1) singlet as the sensing resource; quantify with von Neumann entropy; extract
   **dominant natural orbitals** to define reference `|S*⟩`, `|T₀*⟩`.
3. **Signal encoding.** A static **magnetic-field gradient** `δB = B_L − B_R` drives coherent
   singlet↔triplet mixing: `⟨T₀|H_B|S⟩ = gµ_B δB/2`. Effective two-level model with coupling
   `λ(δB) = (gµ_B δB/2)M_ge`, `M_ge = ⟨e|S^z_L−S^z_R|g⟩`, splitting `Δ_ST`; transition probability
   `P_{g→e}(t)` (two-level Rabi form).
4. **Metrology.** Quantum Fisher information
   `F_Q^{ST}(t) = [4(gµ_B)²|M_ge|²/Δ_ST²] sin²(Δ_ST t/2ℏ)` and classical FI for the binary
   singlet–triplet readout (with characteristic **dips** where the readout is locally insensitive);
   quantum Cramér–Rao bound `Var ≥ 1/(νF_Q)`.
5. **Benchmark & gain.** Independent-spin Ramsey benchmark `F_Q^{ind} = ½(gµ_B t/ℏ)²`. For an ideal
   pair `M_ge=1`, `F_Q^{ST} = 2 F_Q^{ind}` — a **factor-of-2** QFI gain (the N=2 instance of
   Heisenberg scaling). In full CI, reduced by `|M_ge|²` and finite detuning (relative difference from
   ×2 is <1% at optimum).
6. **RL optimization.** Actor–Critic **PPO** over the four/seven electrode voltages, maximizing a
   Fisher-information-based reward `R(a) = r_f·r_cfi − (ω_µ p_µ + ω_b p_b)` combining singlet/triplet
   fidelities and two-/three-channel classical FI, with penalties on delocalized orbitals and low
   barrier. Hyperparameters in the paper's Table 1.
7. **Networks (proposal).** Extend to arrays: singlet is optimal for gradients (generator `G₋`),
   Bell/GHZ for common-mode (`G₊`); each reaches `F_Q ∝ N²` for its generator. Unifying quantity:
   QFI; unifying resource: variance of the field-coupling generator.

## Discussion / implementation
Sensing mode (Ramsey/parity readout, common-mode rejection), readout (cQED + image-charge; spin via
spin-to-charge), integration into cryogenic HEP experiments, and challenges (cryogenics, single-
electron control, readout fidelity, fabrication/scalability, signal coupling through superconducting
shielding).

## Honest framing (carry into new work)
- The demonstrated advantage is a **fixed factor of 2** for two electrons, not a scaling
  demonstration; the network `1/N` claim is a proposal.
- Static-gradient case only; **time-dependent fields are future work**.
- Spin readout and long spin coherence on eHe are **predicted/proposed**, not measured.

## Related skills
`quantum-sensing` (primary), `coulomb-entanglement`, `two-qubit-gates`, `ci-dvr-hartree-numerics`,
`platform-electrons-on-helium`.
