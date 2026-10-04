# Resume — Mohamed Aziz Kammoun

A personal Quarto resume based on the supplied `Resume` folder.

## Editing

`index.qmd` is the canonical resume source. Edit the summary, skills, projects,
experience, and education there. `source/cv_2.tex` and `source/res.cls` preserve
the original LaTeX files for reference and are not part of the Quarto build.

The Projects section includes MindFlow, FIN-SHIELD, IEEE Tunisia Partnership Hub,
Hackership-AI, HealFlow, MedAI Nexus, and three earlier projects. For upcoming projects, provide the
name, repository or demo link, technologies, your role, and concrete achievements.
Include dates and measurable results when known. Do not invent missing details.

## Build

Requires Quarto and a LaTeX distribution for PDF. If needed, run
`quarto install tinytex`.

```sh
quarto preview index.qmd --to html
quarto render
```

Outputs: `_output/resume.html` and `_output/resume.pdf`.

```sh
quarto render index.qmd --to html
quarto render index.qmd --to pdf
```

`styles.css` controls HTML and browser printing; `resume-header.tex` controls
PDF styling. This full CV may span multiple pages; select fewer projects for a
shorter job-specific version. Build output and caches are ignored by Git.
Repository: [ASHEN-IX/resume](https://github.com/ASHEN-IX/resume).
The local folder is `my resume`.
