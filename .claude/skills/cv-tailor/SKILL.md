---
name: cv-tailor
description: Tailors a concise, truthful markdown CV from master/master-cv.md for a specific job description. Use whenever the user asks to tailor, generate, or update a CV/resume for a job, or points at a folder under jobs/. Runs a 5-stage pipeline writing numbered stage outputs into the job folder.
---

# CV Tailor

Generate a tailored, to-the-point CV in markdown from the user's master CV and a job description.

## Core principles (non-negotiable)

1. **Truth-preserving.** Never invent, inflate, or imply experience not present in `master/master-cv.md`. Reframing and emphasis are allowed; fabrication is not. Every claim in the final CV must be traceable to the master CV.
2. **Stages write files.** Each stage writes its output file into the job folder BEFORE the next stage begins. Never skip a stage or hold results only in conversation.
3. **Brevity rules win.** `references/writing-rules.md` overrides any stylistic instinct. When in doubt, cut.
4. **Master data is read-only.** Never edit anything under `master/` without explicit user approval. If a discovery conversation surfaces new experience, propose an addition and wait for approval.

## Inputs

- `master/master-cv.md` — exhaustive career record (single source of truth)
- `master/profile.md` — visibility rules, preferences, exclusions
- `jobs/<job-folder>/jd.md` — the job description

If any input is missing, stop and ask the user for it.

## Pipeline

### Stage 1 — JD Analysis → `01-analysis.md`

Read `jd.md` and produce a structured analysis:

- **Must-haves**: explicit hard requirements, quoted or closely paraphrased
- **Nice-to-haves**: preferred qualifications
- **ATS keywords**: flat lowercase list of terms to mirror (skills, tools, methods)
- **Seniority & scope signals**: IC vs lead, team size, ownership language
- **What they're really hiring for**: 2–3 sentences reading between the lines (repeated themes, pain points)

Do not consult the master CV in this stage.

### Stage 2 — Matching & Gap Report → `02-matching.md` [CHECKPOINT]

Map each must-have and nice-to-have from `01-analysis.md` against `master/master-cv.md`, honoring visibility rules in `master/profile.md`:

| Requirement | Evidence in master CV | Confidence (high/med/low) | Notes |

Then list:
- **Gaps**: requirements with no honest evidence. Never propose covering a gap with fabricated content; suggest adjacent honest framing or note it as a genuine gap.
- **Excluded content**: master-CV items deliberately left out, each with a one-line reason.

**Stop and show the user this file. Wait for approval or corrections before Stage 3.**

### Stage 3 — Draft → `03-draft.md`

Write the tailored CV using ONLY high/medium-confidence matched content from `02-matching.md`. Follow `templates/cv-structure.md` for structure and `references/writing-rules.md` for style, strictly. Weave ATS keywords in naturally where truthful — never keyword-stuff.

### Stage 4 — Review → `04-review.md` [CHECKPOINT]

Critique the draft against three checklists and record results:

1. **Truthfulness**: every line traceable to master CV? List any line that is not.
2. **Style compliance**: run through every rule in `writing-rules.md`; list violations.
3. **ATS coverage**: table of keywords from `01-analysis.md` → present in draft? yes/no. Report coverage %. Follow `references/ats-scoring.md` for method and interpretation thresholds.

Fix all violations in the draft, then **show the user the review and revised draft. Wait for approval.**

### Stage 5 — Finalize → `cv.md` + `cv.yaml`

On approval, write the final version to `cv.md` in the job folder. Also write
the same content as `cv.yaml`, following the schema in
`.claude/skills/resume-formatter/references/yaml-schema.md` — `cv.md` stays
the readable source of truth, `cv.yaml` is what the resume-formatter skill
renders to PDF. Offer (but do not run unprompted) formatting via the
resume-formatter skill.

## Re-running stages

The user may ask to re-run from any stage ("redo the draft, matching was fine"). Read the existing upstream stage files as inputs and only regenerate downstream files.
