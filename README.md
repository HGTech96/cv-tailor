# cv-tailor

Local, Claude Code-driven CV tailoring: master CV + job description -> concise markdown CV
through a 5-stage inspectable pipeline, with optional PDF formatting and visual QA.

## Quick start
1. Fill in `master/master-cv.md` (be exhaustive) and `master/profile.md`.
2. Copy `jobs/_example-job` to `jobs/YYYY-MM-company-role/` and paste the JD into `jd.md`.
3. Run `claude` in the repo root and say:
   "Tailor my CV for jobs/<folder>. Follow the cv-tailor skill stages in order."
4. Review at the two checkpoints (after matching, after review). Final CV lands in
   `cv.md` (and `cv.yaml`, the structured version used for PDF formatting).
5. Optional: ask to format `cv.yaml` to PDF via the resume-formatter skill (needs
   `typst` installed — see `.claude/skills/resume-formatter/SKILL.md`), then ask
   for a visual QA pass via the resume-reviewer skill.

## Pipeline outputs per job
01-analysis.md -> 02-matching.md [checkpoint] -> 03-draft.md -> 04-review.md [checkpoint] -> cv.md + cv.yaml -> (optional) PDF

## Tuning
Fix recurring problems in `.claude/skills/cv-tailor/references/writing-rules.md`
or `master/profile.md`, not in individual CVs.

## Credits
Pipeline design adapted from varunr89/resume-tailoring-skill (MIT) with
master-profile and ATS-scoring patterns inspired by olegvg/resume-tailor-plugin.
