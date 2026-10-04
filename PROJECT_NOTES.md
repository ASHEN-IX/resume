# Project review notes

Reviewed on 2026-10-04. These notes record evidence used to write project bullets;
they are not rendered into the resume. Project ownership follows the user's
identification of these as their projects; code review does not establish each
individual contribution. No project application tests were run for this CV edit.

- **MindFlow:** `../..` workspace sibling `mindflow/`: docs-repo README,
  implementation tracker, study-partner-api README, web package manifest,
  Python planner and signal-processing code. Eight Node services plus Python AI;
  RAG planning and focus/fatigue adapters are present. Team of seven comes from
  the originally supplied CV. Graph RAG is planned and is not claimed.
- **HealFlow:** `healflow/healflow/`: README, pyproject, PipelineGuard,
  ContractValidator, Pandas adapter, unit/integration test sources. Current v0.1
  supports deterministic validation; autonomous or AI healing is not implemented.
- **Hackership-AI:** `hackership/hackership-ai/`: README, MyWork.md,
  implementation/delivery reports, requirements, taxonomy, and test sources.
  The main `app/` directory is missing in this local snapshot. Descriptions are
  grounded in documented delivery and test contracts, without unverified speed,
  coverage, or production-readiness metrics. No repository link was supplied.
- **IEEE Tunisia Partnership Hub:** README, package manifests, module/service
  layout and API domain source. Local Git origin is
  https://github.com/GitHackerz/ieee-tunisia-partnership-hub; omitted from the CV
  because public accessibility was not verified. Current platform is an alpha.
- **FIN-SHIELD:** https://github.com/ASHEN-IX/Fin-shield, reviewed via public
  GitHub and a shallow clone at `/tmp/cv-fin-shield-review`. README,
  api/app/analytics/mock.py, agent README and agent/app implementation.
  The web/API demo uses deterministic mock analytics. A separate investigation
  agent and lexical document retrieval exist; this is not a deployed trained-model
  fraud detector. Human analysts retain decisions. Conflicting older README
  status text was resolved against the current code and detailed agent docs.

Nova Sandbox, RepoRadar, and Hikma Learn were removed from the Projects section.
Hikma Learn initially remained in the internship history; the subsequent
internship correction below supersedes that history.
The original LaTeX reference files are preserved unchanged in `source/`.

## Subsequent user updates

- Replaced Code Review Buddy with MedAI Nexus (`medical-ai`). Public repository
  README and shallow clone (`/tmp/cv-medical-ai-review`) were reviewed,
  including AI service route registrations, model services, frontend intake,
  and the NestJS package manifest. The README describes an integrated local prototype with a Next.js/NestJS/FastAPI
  architecture, diabetes decision-tree model, autism survey model, and kidney
  model integrations. Do not claim clinical validation or production deployment;
  the image-based autism model depends on external model artifacts.
- The user explicitly confirmed leading developer teams for Medical AI,
  Hackership-AI, and MindFlow. Added leadership to all three project entries.
  Kept the previously supplied MindFlow team size; did not infer other team sizes.
- Changed the IEEE chapter role from Media Manager to Webmaster as requested.
  Existing tenure and responsibilities remain sourced from the supplied CV.

## Internship correction

The user identified MindFlow as the first internship of this summer at ESPRIT
TECH, where they led the developers, and Felcloud as the second internship.
Replaced the previous Hikma Learn internship and generic University Projects
experience with these two internship entries. Summer 2026 follows the user's
"this summer" and the current date. The user subsequently confirmed July–August for both internships.
Felcloud project duties have not yet been supplied and are omitted. MindFlow's team of
seven and platform architecture come from the supplied CV and project review.

## Third internship restored

The user clarified that there are three internships. Restored the original
ESPRIT TECH / Hikma Learn internship for July–August 2025, using the originally
supplied CV, alongside MindFlow and Felcloud (July–August 2026). This supersedes
the earlier removal of that internship. Hikma Learn remains excluded from the
Projects section as requested.

## Felcloud internship details and ordering

The user confirmed that Hackership was developed during the Felcloud internship
and requested the order Hikma Learn, MindFlow, Felcloud. The Felcloud entry now
uses Hackership README and MyWork.md: AI task decomposition, mission generation,
resume extraction, taxonomy-normalized skills, weighted matching, and Redis
caching. Team leadership was confirmed earlier by the user. The documented
matching feature used mocked developer profiles, so no live GitHub profile
integration or production deployment is claimed. This supersedes the previous
note that Felcloud duties were unspecified.
