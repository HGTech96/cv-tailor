# cv-tailor

This repo tailors concise markdown CVs from a master CV for specific job descriptions,
and can optionally format the result into a print-ready PDF and QA it.

## Layout

- `master/master-cv.md` — exhaustive career record. **Read-only: never edit without explicit approval.**
- `master/profile.md` — visibility rules and preferences. Same read-only rule.
- `jobs/<YYYY-MM-company-role>/` — one folder per application, containing `jd.md` plus pipeline outputs.
- `.claude/skills/cv-tailor/` — the tailoring skill (JD → `cv.md` + `cv.yaml`). Its SKILL.md defines the pipeline.
- `.claude/skills/resume-formatter/` — optional: `cv.yaml` → PDF via Typst templates.
- `.claude/skills/resume-reviewer/` — optional: visual QA checklist for the compiled PDF.
- `templates/cv-structure.md` — fixed CV skeleton.

## Workflow

To process a job: the user creates a job folder with `jd.md`, then asks to tailor.
Run the cv-tailor skill stages **in order**, writing each numbered output file
(`01-analysis.md` → `04-review.md`) into the job folder before the next stage.
Stop at the checkpoints after Stage 2 and Stage 4 for user review.
Stage 5 writes `cv.md` and `cv.yaml`; only run resume-formatter (and then
resume-reviewer) if the user asks for a PDF — never unprompted.

## Rules

- Follow `.claude/skills/cv-tailor/references/writing-rules.md` strictly in all CV output.
- Never fabricate experience. Everything in a CV must trace to `master/master-cv.md`.
- If the user asks to fix a recurring output problem, prefer proposing an edit to
  `writing-rules.md` or `profile.md` over one-off fixes.
