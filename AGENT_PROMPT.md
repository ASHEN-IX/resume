# Agent Prompt — Fill the Quarto Report Template

> Paste this whole document (this file is `AGENT_PROMPT.md`) into your AI
> coding agent, or point the agent at this repository's root and tell it to
> start by reading this file. It contains everything the agent needs, in a
> fixed order, so it can run start-to-finish without asking clarifying
> questions.

---

## Your task

You are preparing a professional PDF internship/project report. A Quarto report
**template** lives in this repository. Your job is to:

1. **Collect** the project facts (by asking the user only the minimal necessary
   questions, with sensible defaults).
2. **Substitute** every `{{VARIABLE}}` placeholder across all `.qmd` files.
3. **Write** real chapter content into every `<!-- TODO: ... -->` block.
4. **Verify** the images, tables, acronyms and the bibliography.
5. **Render** the final PDF and confirm it is clean (no leaks, no broken
   tables, letters A/B for appendices).

Do **not** restructure the book, renumber chapters, or invent a new
architecture. Fill the template that exists.

---

## Step 0 — Read these files first

Read, in this order, before doing anything else:

| Order | File                     | Why                                   |
|------:|--------------------------|---------------------------------------|
| 1     | `template.yaml`          | Every variable + default + example.   |
| 2     | `_quarto.yml`            | Book config: chapters, filters, font, |
|       |                          | PDF/LaTeX header-includes.            |
| 3     | `acronyms.yml`           | The acronym list the filter resolves. |
| 4     | `index.qmd`              | Front matter, intro, `\printacronyms`.|
| 5     | `Chapter-1.qmd` … `Chapter-4.qmd`, `conclusion.qmd`, `Code.qmd`, `Screenshots.qmd` | The chapters. |

## Step 1 — Collect the variables

For each key in `template.yaml`, ask the user only if the project truly needs
it. Use these rules:

- Use the `default:` when the user has no preference.
- Tease out missing background (organization, program, supervisor, dates)
  with a single consolidated question — **one message, not a drip-feed**.
- If the user says "just use what makes sense", use examples from
  `template.yaml` and proceed.

While collecting, note chapter-specific content needs (see Step 3) so you can
ask for any facts you will need while the conversation is open.

## Step 2 — Substitute variables

1. Every `{{VARIABLE}}` in every `.qmd`, `_quarto.yml`, `acronyms.yml`,
   `references.bib` and `template.yaml` must become concrete text. Keep a
   check-list; a leaked `{{...}}` is a render error.
2. For every `\acr{KEY}` / `\acrs{KEY}` used in your content, confirm the key
   exists in `acronyms.yml`. Add missing keys (alphabetical). Delete keys you
   never use — Quarto warns on unknown keys.
3. Keep the existing cross-reference IDs (`#sec-*`, `#fig-*`, `#tbl-*`). If
   you rename a section heading, keep its `{#sec-*}` anchor so `@sec-*`
   citations elsewhere keep resolving.
4. Keep every `{{...}}`-driven structure (table colwidths, appendix labels,
   header-includes). Do not "simplify" the LaTeX that was hard-won.

## Step 3 — Write chapter content

Each chapter ships with `<!-- TODO: ... -->` blocks. Replace every one with
real prose, following the pattern already present in each chapter:

### Conventions to keep everywhere

- **First-use acronyms**: use `\acrs{KEY}` the first time, `\acr{KEY}` after.
- **Cross-references**: `@sec-...`, `@fig-...`, `@tbl-...`, `@eq-...` — never
  hardcode numbers ("see Section 2.3" is forbidden; use `@sec-...`).
- **Figures**: one image per line, caption + `{#fig-...}` anchor + dimensions
  attribute (`width=85%`, `fig-pos="H"`). Keep image files in `assets/`.
- **Tables**: pipe syntax with a `: Caption {#tbl-... tbl-colwidths="[...]"}`.
  **For any cell containing a long monospace/path token** (API path, class
  name, identifier), split it at a logical separator with a forced LaTeX
  line break so it never overflows the column:
  - at `/` boundaries in paths, e.g.
    `/api/v1/task-decomposer/` `\newline`{=latex} `decompose`
  - at `_` boundaries in identifiers, e.g.
    `frameworks_and_` `\newline`{=latex} `technologies`
  - Test renders (this template adds
    `\AtBeginEnvironment{longtable}{...\hyphenpenalty=10000}`) so tokens that
    cannot fit will **not** be hyphenated mid-word — you must provide the
    manual break, Quarto will not do it for you.
- **Code listings**: fenced blocks with language hint. **CRITICAL — the two
  bugs this template was built to prevent:**
  1. Never leave a code fence unclosed. Every fenced block must be closed
     with ```` ``` ```` (the appendix code file must end with the closing
     fences + a trailing newline). An open fence swallows Quarto's appended
     file-metadata comments into the listing and they render as visible
     "garbage" text in the PDF.
  2. Keep code lines short enough to wrap cleanly (break long lines into two
     statements instead of letting LaTeX wrap mid-line).
- **LaTeX in cells**: after any token that must not re-hyphenate use
  `\textsubscript`/no-break spaces carefully; prefer explicit `\newline`{=latex}`.

### Table numbering note

The appendix-chapter boundary is a `longtable`/`appendix` transition. Quarto
numbers appendices with **letters** (A, B) only when each appendix file runs
end-to-end with no trailing content. Do not append to an appendix file after a
figure/code block and do not leave the last fence open — otherwise appendix
letters silently become chapter numbers (5, 6) and `<!-- quarto-file-metadata`
comments leak into the body text.

### Per-chapter focus

- **Chapter 1** — internship/project context, motivation, problem in the
  field, existing solutions, the proposed solution, objectives, methodology.
- **Chapter 2** — stakeholder analysis, standards, functional + non-functional
  requirements (tables 2.x), use cases, backlog.
- **Chapter 3** — architecture, domain/entity model, API design
  (@tbl-api-endpoints with the documented `\newline` path-splitting rules),
  UI/UX, technology choices, AI integration design.
- **Chapter 4** — the implementation chapter: environment/tools, each module's
  implementation, and the main code snippets (move real common algorithms into
  `Code.qmd` Appendix A).
- **conclusion.qmd** — short wrapping summary.
- **Screenshots.qmd** — replace the placeholder screenshots with real
  platform screenshots, one figure per line.

## Step 4 — Clean-up checklist (before rendering)

- [ ] No `{{VARIABLE}}` left anywhere (`grep -rn "{{" *.qmd _quarto.yml`).
- [ ] Every `<!-- TODO: -->` block replaced or deliberately removed.
- [ ] All referenced images exist (run the template's
      `verify-assets` step — diagrams + screenshots referenced a file).
- [ ] `acronyms.yml` contains every acronym key used; unused keys removed.
- [ ] `references.bib` + every `[@key]` citation in text is defined.
- [ ] Every ```` ``` ```` fence has both open and close marks.

## Step 5 — Render and verify

```bash
quarto render
```

Then **verify the output, not just that Quarto exited 0**:

```
# appendix letters, not numbers:
pdftotext -layout _book/*.pdf - | grep -nE "^A (Code|Platform)|^B " 
#   ^ should show A Code, B ... — if you see "5 Code / 6 ..." the appendix
#     boundary broke; re-check the last code fence in Code.qmd / Screenshots.qmd

# no metadata comment leaks:
pdftotext -layout _book/*.pdf - | grep -c "quarto-file-metadata"   # must be 0

# no stray placeholders rendered:
pdftotext -layout _book/*.pdf - | grep -nE "\{\{|\}\}"             # must be 0

# no mid-token hyphenation splits in longtable cells (e.g. a broken:
#   "Task De-composer" across two lines means a token overflowed its column;
#   add a \newline break).
```

Open the PDF in a viewer and spot-check the API table (@tbl-api-endpoints),
the capability table, and the confidence table — these are the places the
original report had overflow issues. Scroll through `A.5` (the email worker
listing) to confirm no trailing metadata comment text appears after the code.

Only when all checks pass, report success with the PDF path and page count.

---

## Step 6 — Hand-off summary

Report back:

- the final `_book/*.pdf` path and page count
- which variables you changed (and which defaults you accepted)
- any TODO blocks you left (files + what is still needed)
- any risks you noticed (e.g., a table that is tight, an acronym list that
  needs more entries)

---

*This file is part of the `quarto-report-template` — edit it freely whenever
your filling workflow changes.*