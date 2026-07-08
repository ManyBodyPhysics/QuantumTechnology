# Electrons on Helium — Quantum Gates, Entanglement, Sensing & Readout

A research-project workspace and **Claude Project skill set** for quantum information and quantum
sensing with **electrons trapped on superfluid helium** (and closely related systems: semiconductor
quantum dots, double quantum dots, solid-neon electrons). It bundles the group's five core papers —
three theory papers and two experimental resonator-readout papers — distilled skill files that let
Claude reason accurately about the physics and numerics, and a scaffold for new code, notebooks, and
manuscripts.

The scope, as the project grows: **making quantum gates, entanglement, quantum sensing, basic
features of quantum-dot systems, electrons trapped on helium, resonator-based readout, and similar
systems** — plus new ideas built on top of these.

## What's inside

```
electrons-on-helium-quantum/
├── README.md                     ← you are here
├── CONTRIBUTING.md               ← how to add skills / papers / code / ideas
├── LICENSE                       ← MIT (code & skill text); papers keep their own copyright
├── .gitignore
├── skills/                       ← Anthropic-style Agent Skills (SKILL.md + references/)
│   ├── platform-electrons-on-helium/    ← the shared physical picture (start here)
│   ├── quantum-dots-primer/             ← semiconductor QD / DQD background & fair comparison
│   ├── coulomb-entanglement/            ← entanglement generation, Hartree/CI, configs I/II/III
│   ├── two-qubit-gates/                 ← √iSWAP / CZ gate design, fidelity, screening/decoherence
│   ├── quantum-sensing/                 ← singlet–triplet sensor, Fisher info, RL, networks
│   ├── resonator-coupling/              ← high-impedance SCR design, TiN, coupling-strength g
│   ├── charge-readout/                  ← demonstrated dispersive charge sensing/control above 1 K
│   ├── ci-dvr-hartree-numerics/         ← the computational toolkit (+ code templates)
│   └── literature-and-notation/         ← shared units/notation, paper map, references.bib
├── papers/                       ← the five source PDFs …
│   ├── 2024_Beysengulov_coulomb-entanglement_PRXQ5.pdf
│   ├── 2026_Leinonen_two-qubit-gates_PRA113.pdf
│   ├── 2026_Perruzza_quantum-sensing-eoh.pdf
│   ├── 2025_Koolstra_high-impedance-resonators_PRApplied23.pdf
│   ├── 2025_Castoria_single-electron-sensing-above-1K_PRX15.pdf
│   └── summaries/                ← … and structured markdown summaries of each
├── projects/                     ← early-stage manuscripts for NEW (unpublished) research ideas
│   ├── _template/                       ← copy this to start a new project
│   ├── majorana-two-electron-sensor/    ← eHe singlet sensor repurposed for Majorana zero modes
│   ├── rl-agentic-quantum-control/      ← RL/agentic optimization for gates and sensing
│   ├── optomechanics-analogues/         ← sideband cooling / squeezing / entanglement analogues
│   └── time-dependent-field-sensing/    ← static-gradient sensor extended to oscillating/transient
│                                           particle-physics fields (axion/ALP, dark photon, EDM, ...)
├── notebooks/                    ← Jupyter notebooks / Jupyter-book chapters (scaffold)
└── src/                          ← Python-first library; C++/Fortran kernels (scaffold)
```

## The five core papers

Three **theory** papers share one device and CI backbone (Oslo group). Two **experimental** papers
(EeroQ Corporation collaboration, overlapping authorship) demonstrate the microwave-resonator readout
hardware those proposals assume — on their own, separate device geometry. See
`skills/literature-and-notation/references/paper-map.md` for the full cross-reference, including the
note on keeping the two device families distinct.

| Key | Paper | Venue | Skill |
|---|---|---|---|
| `beysengulov2024` | Coulomb Interaction-Driven Entanglement of Electrons on Helium | PRX Quantum 5, 030324 (2024) | `coulomb-entanglement` |
| `leinonen2025` | Design and dynamics of two-qubit gates with motional states of electrons on helium | Phys. Rev. A 113, 032624 (2026) | `two-qubit-gates` |
| `perruzza2026` | Electrons on Helium and Entangled Quantum Sensors for Particle Physics | 2026 (CERN DRD5) | `quantum-sensing` |
| `koolstra2025impedance` | High-Impedance Resonators for Strong Coupling to an Electron on Helium | Phys. Rev. Appl. 23, 024001 (2025) | `resonator-coupling` |
| `castoria2025` | Sensing and Control of Single Trapped Electrons above 1 K | Phys. Rev. X 15, 041002 (2025) | `charge-readout` |

The theory trio shares one device and CI backbone: `beysengulov2024` defines the entangled
**configurations I/II/III**, `leinonen2025` drives them in time to make **gates**, and `perruzza2026`
uses the entangled states as a **sensor**. The experimental pair grounds the readout side:
`koolstra2025impedance` engineers the **coupling strength** toward strong coupling, and `castoria2025`
**demonstrates** dispersive charge detection and deterministic single-electron control — at
temperatures (>1 K) well above typical dilution-fridge cQED.

## How the skills fit together

```
                       platform-electrons-on-helium  ── shared physical picture
                                    │
        quantum-dots-primer ────────┼──────── literature-and-notation (units, notation, refs)
                                    │
                        coulomb-entanglement  ── entangled states, Hartree/CI, configs
                            │             │
                   two-qubit-gates   quantum-sensing
                            └──────┬──────┘
                          ci-dvr-hartree-numerics  ── grids, CI, propagation, Fisher info, RL

                       resonator-coupling ──── charge-readout
                       (coupling-strength g)   (demonstrated dispersive
                                                 sensing & control, >1 K)
                          — the experimental readout backbone, referenced
                            from platform-electrons-on-helium and quantum-sensing —
```

Each `SKILL.md` has a "pushy" description so Claude consults it at the right time, keeps its body
focused, and pushes heavy detail into `references/` files (progressive disclosure).

## New projects (first round)

`projects/` holds early-stage manuscripts for research directions that don't have results yet —
title, abstract sketch, motivation, and an outlined model, using REVTeX 4-2 templates consistent
with the group's existing APS-journal manuscripts. See `projects/README.md` for conventions.

| Folder | Working title | Builds on |
|---|---|---|
| `majorana-two-electron-sensor/` | Two electrons on helium as a differential sensor for Majorana zero modes | `quantum-sensing`, `coulomb-entanglement` |
| `rl-agentic-quantum-control/` | Reinforcement learning and agentic optimization for quantum gates and quantum sensing | `two-qubit-gates`, `quantum-sensing`, `ci-dvr-hartree-numerics` |
| `optomechanics-analogues/` | Optomechanical analogues on helium: sideband cooling, motional squeezing, motional entanglement | `resonator-coupling`, `charge-readout`, `coulomb-entanglement` |
| `time-dependent-field-sensing/` | Beyond the static gradient: electrons on helium as a time-dependent-field sensor for particle physics | `quantum-sensing`, `coulomb-entanglement`, `ci-dvr-hartree-numerics` |

These are proposals, not results — each `main.tex` is explicit about what's established vs. open.
Code for these projects belongs in the existing shared `src/` and `notebooks/` trees (Python first,
C++/Fortran object-oriented for hot kernels, Jupyter notebooks/Jupyter-book for narrative), not in a
separate per-project code tree.

## Using this as a Claude Project

1. **Create a Project** in Claude and add the five PDFs in `papers/` (and, if useful, the markdown
   summaries) as project knowledge.
2. **Add the skills.** Point the project at `skills/` (or upload/package individual skills). Each
   skill is a folder with a `SKILL.md`; the numerics and literature skills also carry `references/`.
3. **Connect GitHub** so the project tracks this repo (see below). New skills, notebooks, and code
   land in the repo and flow back into the project.

> Tip: the skill descriptions are tuned to trigger on natural phrasings ("how does the helium trap
> work", "optimize the √iSWAP ramp", "what's the Fisher information gain", "how strong is the
> electron–photon coupling", "how do we count electrons in the trap") — you don't have to name a
> skill explicitly.

## GitHub integration

This directory is a ready-to-push repository.

```bash
cd electrons-on-helium-quantum
git init
git add .
git commit -m "Initial commit: eHe quantum project (papers + skills + scaffold)"
git branch -M main
git remote add origin git@github.com:<your-org>/electrons-on-helium-quantum.git
git push -u origin main
```

Then connect the GitHub repo to your Claude Project. The PDFs are committed for convenience; if you
prefer to keep large binaries out of git, move them to a release or Git LFS and keep only
`papers/summaries/` in-tree (see `.gitignore` notes).

## Conventions (don't drift)

- Natural units `ℏ²/2mₑ = 1`, `ℏ = 1`; soft Coulomb `κ = 2326`, `ε = 1e-2`; theory-trio device
  geometry fixed (7 electrodes, `d ≈ 1.5 µm`, `h = 500 nm`). The two experimental readout papers
  (`koolstra2025impedance`, `castoria2025`) describe **separate, real EeroQ-collaboration hardware**
  with their own geometry — don't merge the two device families. Full list:
  `skills/literature-and-notation/references/notation.md`.
- Code: **Python** first (NumPy/SciPy); **C++/Fortran (object-oriented)** for hot kernels with parity
  tests; **Jupyter notebooks / Jupyter-book** for narrative and reproducible figures.
- Claims discipline: mark predicted/proposed results (long spin coherence, network `1/N` scaling,
  simulated-but-unmeasured coupling strengths) as such; keep closed-system gate fidelities labeled as
  upper bounds; keep demonstrated readout results (`castoria2025`) distinct from design/roadmap
  results (`koolstra2025impedance`).

## Roadmap (edit freely)

- [ ] Populate `src/` with the reference Python implementation (DVR → Hartree → CI → propagation → FI).
- [ ] Add the six starter notebooks (see `notebooks/README.md`) and wire up a Jupyter-book.
- [x] Add skills grounding the resonator readout hardware: `resonator-coupling` (impedance/coupling
      design) and `charge-readout` (demonstrated dispersive sensing/control above 1 K).
- [x] Scaffold `projects/` with LaTeX (REVTeX 4-2) templates, seeded references, and initial
      motivating text for four new directions: Majorana-mode sensing, RL/agentic control,
      optomechanics analogues, time-dependent-field particle-physics sensing.
- [ ] Develop each `projects/` idea past its first open question (see each project's `notes.md`);
      promote to a `skills/<slug>/SKILL.md` once there's real content to distill.
- [ ] Add skills for new directions: time-dependent-field sensing (see
      `projects/time-dependent-field-sensing/` for the literature-search starting point),
      sensor-network design, spin readout / spin-to-charge, error/decoherence modeling (Lindblad —
      also needed by `optomechanics-analogues`), solid-neon electrons.
- [ ] Optional: run the skill-creator eval loop to tune skill triggering once usage patterns emerge.

## License & attribution

Code and skill text: MIT (`LICENSE`). The bundled PDFs remain under their publishers'/authors'
copyright and are included for research convenience — cite the papers, not this repo, for their
results (`skills/literature-and-notation/references/references.bib`).
