# Project template

Copy this folder to start a new project: `cp -r projects/_template projects/<slug>`.

- `main.tex` — REVTeX 4-2 manuscript scaffold. Pick class options for the target journal (see
  comments at the top of the file).
- `references.bib` — project-local bibliography; seed it with the relevant subset of the master
  bib (`skills/literature-and-notation/references/references.bib`) plus new sources as you find
  them. Copy anything new back into the master bib once it proves out (see root `CONTRIBUTING.md`).
- `notes.md` — informal brainstorm/outline space: open questions, equations to work out, related
  skills, before committing prose to `main.tex`.

Compile with `latexmk -pdf main.tex`, or `pdflatex main.tex && bibtex main && pdflatex main.tex
&& pdflatex main.tex`.
