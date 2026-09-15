# Quarto Report Template

A ready-to-use **Quarto book** template for internship reports, project
reports, and AGM-style deliverables. It is a stripped-down, generalized
version of a real two-month internship report ("Hackership AGM: An AI
Orchestration Platform for Internship Management"), keeping the structural
patterns and tooling while making all content replaceable.

Clone this repository every time you need a new report/report chapter pack,
then either fill the placeholders by hand or hand it to an AI coding agent to
generate the content for you.

## What you get

- A **4-chapter book** (presentation → analysis → design → implementation)
  plus conclusion, references, and two appendices (code + screenshots).
- **Quarto + PDF (LaTeX)** output with a professional look: KOMA-Script
  `scrreprt`, fancy headers/footers, an acknowledgements page, introduction,
  list of acronyms, table-of-contents, bibliography, and cross-referenced
  figures/tables/equations.
- **Acronyms management** via the `rchaput/acronyms` Quarto extension
  (shortcodes `\acr{}` and acronym definition file `acronyms.yml`).
- **IEEE-style citations** with URLs (`ieee-with-url.csl` + `references.bib` +
  `references.qmd`).
- **`template.yaml`** — a machine-readable inventory of every
  `{{VARIABLE}}` to substitute TeX/Quarto/internship metadata in the source.
  An AI agent reads this file to know exactly what to ask you and where
  placeholders must be filled.
- Placeholder PNG images so the book renders without missing files.

## Repository layout

```
.
├── _quarto.yml            # Book config (title, chapters, appendices, format)
├── template.yaml          # Every variable the agent must collect+replace
├── acronyms.yml           # Acronym definitions (acronyms filter)
├── references.bib         # BibTeX bibliography (cited via [@key])
├── references.qmd         # Bibliography appendix (unnumbered)
├── ieee-with-url.csl      # IEEE citation style (with URLs)
├── index.qmd              # Acknowledgements + Introduction + \printacronyms
├── Chapter-1.qmd          # Project presentation
├── Chapter-2.qmd          # Analysis & requirements
├── Chapter-3.qmd          # Design
├── Chapter-4.qmd          # Implementation
├── Code.qmd               # Appendix: code excerpts
└── Screenshots.qmd        # Appendix: platform screenshots
```

## Quick start (human)

1. Clone this repository.
2. Open `template.yaml`, and for each variable write the value for your
   project (title, author, organization, project names, acronyms, ...).
3. Run a global find-and-replace of every `{{VARIABLE}}` token in the
   `.qmd` files with those values.
4. Replace the chapter content, fill the `<!-- TODO: ... -->` blocks,
   and drop your real diagrams/screenshots into `assets/`.
5. Render:

   ```sh
   quarto preview   # live preview
   quarto render    # produce the PDF in _book/
   ```

## Quick start (AI agent)

The template is designed to be consumed by an AI coding assistant. The agent
should:

1. Read `template.yaml` to learn every variable it must collect and its
   default. **Ask the user** for the required values (title, author,
   organization, project name, internship dates, chapters, acronyms, ...).
2. Replace every `{{VARIABLE}}` placeholder across all `.qmd` files with the
   values provided (using defaults where the user has no preference).
3. Fill the `<!-- TODO: ... -->` blocks with the actual report content
   (write it from the user's summary or prior report).
4. Update referenced assets (diagrams, screenshots) or leave placeholders.
5. Run `quarto render` to verify the PDF builds, and iterate.

## Rendering

Requires [Quarto](https://quarto.org) and a LaTeX engine. The configuration
in `_quarto.yml` targets `pdf` via `lualatex` (VSCode `.vscode/settings.json`
is included). `format: pdf` uses `scrreprt`, 13pt Latin Modern, numbered
sections, and the acronyms extension.

## Acronyms

Acronyms are defined in `acronyms.yml` and referenced with the shortcodes
provided by the `rchaput/acronyms` extension (see `_extensions/`). Every
acronym used in a chapter should be listed here; the acronyms filter warns
about undefined keys. The list of acronyms is printed automatically on the
page after the introduction via `\printacronyms` in `index.qmd`.

## Placeholder images

The `assets/` directory ships with placeholder PNGs (colored boxes with a
label) so the template renders cleanly before real assets are added. Replace
them with:

- `assets/diagrams/` — your architecture, entity-model, use-case/product
  backlog diagrams.
- `assets/screenshots/` — screenshots of the running platform referenced by
  `Screenshots.qmd`.

## TODO inside chapters

Every chapter ships with `<!-- TODO: ... -->` comments marking exactly where
content must be written. You can delete any TODO that doesn't apply. Keeping
placeholders as visible markers makes it easy for an AI agent to know what to
generate.

## License / credits

- Report template: MIT — reuse freely.
- Acronyms extension (`rchaput/acronyms`): (c) its authors.
- IEEE CSL (`ieee-with-url.csl`): (c) its authors.