# Contributing

This repo doubles as a Claude Project. Keep it easy for both humans and Claude to navigate.

## Adding a new skill
1. Create `skills/<skill-name>/SKILL.md` with YAML frontmatter:
   ```
   ---
   name: <skill-name>
   description: >-
     What it does AND when to trigger it. Be specific and a little "pushy" about the contexts —
     Claude tends to under-trigger skills. Put ALL "when to use" info in the description.
   ---
   ```
2. Keep the body focused (ideally < ~300 lines). Push long detail into `skills/<skill-name>/references/*.md`
   and point to those files from the body (progressive disclosure).
3. Cross-link related skills by name, and cite papers by their BibTeX key.
4. Match the shared conventions in `skills/literature-and-notation/` (units, symbols). Don't invent
   new notation without adding it there.

## Adding a paper
- Drop the PDF in `papers/` with a descriptive name `YEAR_FirstAuthor_topic_VENUE.pdf`.
- Add a structured summary in `papers/summaries/`.
- Add a BibTeX entry to `skills/literature-and-notation/references/references.bib`.
- Update `skills/literature-and-notation/references/paper-map.md`.

## Starting a new project manuscript
- Copy `projects/_template/` to `projects/<slug>/` (`cp -r projects/_template projects/<slug>`).
- `main.tex` is a REVTeX 4-2 scaffold; pick the class options for the target journal (see comments
  at the top of the file) and fill in title/abstract/authors.
- Seed `references.bib` with the relevant subset of the master bib plus any new sources; copy new
  sources back into the master bib once they prove out (same rule as "Adding a paper" above).
- Use `notes.md` as an informal scratch pad before committing prose to `main.tex`.
- List the project in `projects/README.md`'s table and the root `README.md`'s "New projects" table.
- Once a project has real content (not just an outline), consider promoting it to a
  `skills/<slug>/SKILL.md` following "Adding a new skill" above.

## Adding code
- Python first, in `src/` as importable modules; keep notebooks thin.
- C++/Fortran (object-oriented) only for hot kernels, with parity tests against the Python reference
  (~1e-10 on a small case). See `skills/ci-dvr-hartree-numerics/references/code-templates.md`.

## Claims discipline
Mark predicted/proposed results as such (long spin coherence, network 1/N scaling); label
closed-system gate fidelities as upper bounds. Keep numbers consistent across the repo.
