# projects/ — early-stage manuscripts for new research directions

This is where **new, not-yet-published ideas** get a manuscript scaffold, as opposed to `papers/`
(source PDFs of the five *completed* core papers) and `skills/` (distilled, citable knowledge from
those completed papers). A project folder here is a place to start writing before there are
results to report — title, abstract sketch, motivation, a model outline, and a references list.

## Structure

Each project is a folder under `projects/<slug>/` containing:

```
projects/<slug>/
├── README.md         ← one-paragraph pitch, target journal, status, related skills
├── main.tex           ← REVTeX 4-2 manuscript scaffold (see projects/_template/)
├── references.bib     ← project-local bib: relevant subset of the master bib + new refs
└── notes.md            ← informal outline: open questions, equations to derive, connections
```

Start a new project by copying `projects/_template/` and filling in the placeholders. When you add
a genuinely new citation while writing, add it to **both** the project's local `references.bib`
*and* the master `skills/literature-and-notation/references/references.bib` (see
`CONTRIBUTING.md`) — the project bib is a convenience for standalone compilation, the master bib is
the single source of truth for the whole repo.

## LaTeX conventions

- Class: **REVTeX 4-2** (`revtex4-2`), matching the group's existing APS-journal manuscripts (the
  project history includes reformatting a manuscript from Scientific Reports style into APS
  REVTeX 4.2). The template's class-option comments show how to retarget between PRA / PRApplied /
  PRX Quantum / PRL; swap them for the actual submission target once one is chosen.
- Bibliography style: `apsrev4-2` via `\bibliography{references}` (run `pdflatex` → `bibtex` →
  `pdflatex` ×2, or `latexmk -pdf`).
- Keep notation consistent with `skills/literature-and-notation/references/notation.md`; if a
  project needs a genuinely new symbol, define it there once it stabilizes rather than reinventing
  it per-manuscript.

## Code and notebooks for these projects

Per the group's conventions (**Python** first for orchestration/prototyping, **C++/Fortran**
(object-oriented) for hot kernels, **Jupyter notebooks and Jupyter-book** for narrative/figures —
see `skills/ci-dvr-hartree-numerics` and `src/README.md`), new project code should land in the
existing shared `src/` and `notebooks/` trees rather than spawning a separate code tree per project.
Namespace new modules/notebooks by project (e.g. `src/eoh/majorana.py`,
`notebooks/07_majorana_sensor_signal.ipynb`) so the toolkit stays one coherent library.

## Current projects (first round)

| Folder | Working title | Builds on | Status |
|---|---|---|---|
| `majorana-two-electron-sensor/` | Two electrons on helium as a differential sensor for Majorana zero modes | `quantum-sensing`, `coulomb-entanglement` | idea / outline |
| `rl-agentic-quantum-control/` | Reinforcement learning and agentic optimization for quantum gates and quantum sensing | `two-qubit-gates`, `quantum-sensing`, `ci-dvr-hartree-numerics` | idea / outline |
| `optomechanics-analogues/` | Optomechanical analogues on helium: sideband cooling, motional squeezing, motional entanglement | `resonator-coupling`, `charge-readout`, `coulomb-entanglement` | idea / outline |
| `time-dependent-field-sensing/` | Beyond the static gradient: electrons on helium as a time-dependent-field sensor for particle physics | `quantum-sensing`, `coulomb-entanglement`, `ci-dvr-hartree-numerics` | idea / outline |

None of these have results yet — everything in `main.tex` beyond the introduction/motivation is a
placeholder or an explicitly labeled proposal. Keep the same **claims discipline** used across this
repo (see `skills/literature-and-notation/references/notation.md`): don't let a proposal read as a
result.

## Adding another project

1. `cp -r projects/_template projects/<new-slug>`
2. Fill in `README.md`, the title/abstract/authors in `main.tex`, and seed `references.bib` with the
   relevant subset of the master bib plus any new sources.
3. Sketch the physics in `notes.md` before committing to LaTeX prose.
4. Once the project has real content, consider adding a corresponding `skills/<slug>/SKILL.md` (see
   `CONTRIBUTING.md`) so Claude can reason about its results the way it does for the five core papers.
5. List it in the table above.
