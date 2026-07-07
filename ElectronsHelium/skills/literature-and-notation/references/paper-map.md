# Paper map — which paper has which result

Quick index so new work cites and builds on the right source. PDFs in `papers/`, structured
summaries in `papers/summaries/`.

## `beysengulov2024` — PRX Quantum 5, 030324 (2024)
*Coulomb Interaction-Driven Entanglement of Electrons on Helium.*
- Model Hamiltonian, soft Coulomb (`κ=2326`, `ε=1e-2`), device (7 electrodes).
- Hartree method for distinguishable particles; full CI; sinc-DVR (Colbert–Miller); validation vs
  fermionic CI.
- **Configurations I / II / III**, avoided crossings, von Neumann entropy, Schmidt basis.
- Effective (Bogoliubov) Hamiltonian; **ZZ coupling** `ζ` and its suppression via opposite-sign
  anharmonicities.
- Appendices: electron–ripplon coupling, DVR/Hartree/CI construction, entropy, particle densities,
  optimal well configurations, electrode voltage tables.
- **Use for:** entanglement generation, CI machinery, configuration scheme. → `coulomb-entanglement`.

## `leinonen2025` — Phys. Rev. A 113, 032624 (2026)
*Design and dynamics of two-qubit gates with motional states of electrons on helium.*
- Time-dependent voltage functions `V^β`, `V^ζ`; erf ramp `λ(t)`; configurations I→II/III→I.
- Crank–Nicolson propagation in sinc-DVR product basis; Davidson eigensolve; average gate fidelity
  `F=[Tr(MM†)+|Tr M|²]/20`.
- **√iSWAP:** best `F=0.999` (`V^ζ`, t_gate≈2.9 ns); **CZ:** best `F=0.996` (t_gate≈9.4 ns, `V^β`).
- Swap error vs leakage error; grid-search optimization; ramp/hold stability analysis.
- **Screening** (image charges, `η≈0.69`, gate time ×~1.45) and **decoherence** (charge dephasing
  ~60 MHz; ripplon coupling tunable via `E⊥`).
- Appendices: `V^ζ` optimization, elementwise gate-matrix analysis, full time evolution, screening
  derivation, electron–ripplon Hamiltonian.
- **Use for:** gate protocols, fidelity, robustness, screening/decoherence. → `two-qubit-gates`.

## `perruzza2026` — 2026 manuscript (CERN DRD5)
*Electrons on Helium and Entangled Quantum Sensors for Particle Physics.*
- Sensor concept: entangled singlet as **differential** sensor; DRD5 framing.
- 2D device solve; single-particle spectrum & localized orbitals (sine-DVR, projection localization);
  two-electron CI; dominant natural orbitals; reference `|S*⟩,|T₀*⟩`.
- Signal encoding by magnetic-field gradient; effective two-level model; `P_{g→e}(t)`.
- **Quantum/classical Fisher information**, Cramér–Rao bound; independent-spin **Ramsey benchmark**;
  **factor-of-2** QFI gain (= N=2 Heisenberg).
- **Reinforcement learning (PPO)** trap optimization with FI-based reward (hyperparameters in its
  Table 1).
- From two qubits to **sensor networks**; singlet (gradients, `G₋`) vs Bell/GHZ (common-mode, `G₊`).
- Discussion: sensing mode, readout, integration into HEP experiments, challenges.
- 15 authors; corresponding: Morten Hjorth-Jensen (mhjensen@uio.no). Affiliations: Univ. Agder;
  Univ. South-Eastern Norway; EeroQ; Univ. Oslo; MSU (Physics & Chemistry).
- **Use for:** sensing framework, Fisher information, RL, networks, DRD5 framing. → `quantum-sensing`.

## `koolstra2025impedance` — Phys. Rev. Appl. 23, 024001 (2025)
*High-Impedance Resonators for Strong Coupling to an Electron on Helium.*
- Symmetrically coupled resonator (SCR): common/differential eigenmodes, `C_dot`, inductive-tail
  splitting (`L_t` splits modes with `Z_res,d` unaffected).
- Coupling formula `g = ½eE_xω₀√(Z_res/m_eω_e)`; strong coupling needs `g > κ, Γ` — roughly an
  order of magnitude above prior `g/2π≈5 MHz`.
- TiN fabrication (`L□=178±13 pH/□`), measured `Q_i=3.9×10⁵`, `Z_res≈2.5 kΩ`, `κ_i/2π=11.7 kHz` →
  sevenfold `g` boost vs 50 Ω. Circuit model validated to `<2%` (discount factor `γ≈0.61`).
- Simulated (not yet measured with a real electron): dispersive counting, on-resonance `g/2π=43 MHz`.
- **Use for:** resonator/impedance design, the coupling-strength roadmap. → `resonator-coupling`.
- Device: **EeroQ Corporation** hardware — distinct from the Oslo 7-electrode double well used by the
  three papers above; don't merge geometries/symbols.

## `castoria2025` — Phys. Rev. X 15, 041002 (2025)
*Sensing and Control of Single Trapped Electrons above 1 K.*
- CPW resonator (`f_r=6.04383 GHz`) dispersively coupled to an electrostatic trap decoupled from the
  electron reservoir; demonstrated at `T=1.1 K` (electrons stay bound up to several K, `Δ≈8 K`).
- Electric susceptibility model `χ_e(ω)=Σ_n4g_n²/(ω_n²−ω²+2iωΓ_n)`, shift
  `Δf≈−f_rRe[χ_e(2πf_r)]/2`; single-electron `g_e/2π=9.8 MHz`, two-electron `g_{2+}=√2g_e`.
- **Demonstrated**: bulk (~30e) load/unload, single-electron isolation (discrete `Δf` plateaus,
  `N_e=1..4`), reproducible error-free 1e/2e load–unload cycling.
- Validity at 1 K: plasma parameter `Γ_plasma>30`, no metastable states for `N_e<8`, trap-depth/thermal
  margin ~600×; dominant relaxation is He-vapor-atom scattering, not ripplons.
- **Use for:** dispersive charge sensing, electron counting, deterministic loading/control, elevated-
  temperature operation. → `charge-readout`.
- Device: **EeroQ Corporation** hardware, same collaboration as `koolstra2025impedance` but a
  different specific device (CPW split-ring resonator vs SCR).

## Cross-cutting threads
- **Same device & CI backbone** runs through the first three (theory) papers; keep `κ`, `ε`, geometry
  identical.
- **Configurations I/II/III** originate in `beysengulov2024`, are driven in time in `leinonen2025`,
  and supply the sensing states in `perruzza2026`.
- **Screening & ripplons** are treated most fully in `leinonen2025`; reference it from sensing when
  discussing decoherence/readout.
- **Readout hardware** for the theory/proposal papers is grounded by `koolstra2025impedance`
  (coupling-strength engineering) and `castoria2025` (demonstrated charge detection/control); both are
  EeroQ-collaboration devices, separate from the Oslo 7-electrode device — keep the two hardware
  families distinct even though authorship overlaps (Beysengulov, Pollanen appear across groups).
- **Two senses of "sensing"** coexist in the project: `perruzza2026`/`quantum-sensing` means
  entangled-pair field/particle metrology (HEP framing); `castoria2025`/`charge-readout` means
  resonator-based electron/charge detection (an engineering readout tool). Disambiguate explicitly
  when both could be meant.
