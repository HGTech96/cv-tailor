---
name: resume-formatter
description: Converts resume YAML to professionally formatted PDF using Typst templates. Use when the user wants to generate a PDF, compile their resume, compare template layouts, or create print-ready documents.
---

# Resume Formatter

## Overview

Transform resume YAML files into professionally formatted PDF documents using Typst templates. Choose from 5 templates optimized for different use cases.

## Default templates

Unless the user names a specific template (or asks for "all" / "compare all"),
generate **both Executive and Tech Modern** and hand back both PDFs — these are
the user's preferred pair. Only generate a single template when the user asks
for one by name.

## Quick Start

```bash
# Step 1: Convert YAML to Typst (repeat per template)
python3 scripts/yaml_to_typst.py resume.yaml executive --output resume_executive.typ
python3 scripts/yaml_to_typst.py resume.yaml tech-modern --output resume_tech-modern.typ

# Step 2: Compile each to PDF
python3 scripts/compile_typst.py resume_executive.typ
python3 scripts/compile_typst.py resume_tech-modern.typ

# Result: resume_executive.pdf, resume_tech-modern.pdf
```

## Available Templates

### Template Selection Guide

```
Need?
├─ Professional default → Executive
├─ Modern/creative → Tech Modern
├─ Maximum density → Modern Dense or Compact
└─ Clean/understated → Minimal
```

**Executive** (default)
- Best for: Most professional roles, senior positions
- Style: Clean hierarchy, navy/blue accents
- Font: Inter
- Features: Professional layout, good whitespace balance

**Tech Modern** (new)
- Best for: Modern tech/creative roles, distinctive aesthetic
- Style: Deep lavender palette, pill-style skills, modern typography
- Font: Carlito (Calibri alternative)
- Features: Single-page optimized, creative competency display, professional but contemporary

**Modern Dense** (new)
- Best for: Extensive experience requiring optimal space usage
- Style: Categorized inline skills, tight but readable spacing
- Font: Inter
- Features: Single-page target, 20-25 bullets + summary + skills, strategic density

**Compact**
- Best for: Extensive experience, dense content
- Style: Maximum density without sacrificing readability
- Font: Inter
- Features: Tight spacing, small section headers

**Minimal**
- Best for: Clean, understated presentation
- Style: Monochromatic with single blue accent
- Font: Inter
- Features: Generous whitespace, subtle hierarchy

## Workflow

### Convert YAML to Typst

```bash
python3 scripts/yaml_to_typst.py <yaml_file> <template> --output <output.typ>
```

**Templates:** `executive`, `tech-modern`, `modern-dense`, `compact`, `minimal`

**Options:**
- `--output` / `-o`: Output file path (default: stdout)

**Examples:**
```bash
# Executive template (default)
python3 scripts/yaml_to_typst.py resume.yaml executive --output resume_executive.typ

# Tech Modern template (modern/creative)
python3 scripts/yaml_to_typst.py resume.yaml tech-modern --output resume_tech_modern.typ

# Modern Dense template (maximum density)
python3 scripts/yaml_to_typst.py resume.yaml modern-dense --output resume_modern_dense.typ

# Compact template (dense)
python3 scripts/yaml_to_typst.py resume.yaml compact --output resume_compact.typ

# Minimal template (clean)
python3 scripts/yaml_to_typst.py resume.yaml minimal --output resume_minimal.typ
```

### Compile Typst to PDF

```bash
python3 scripts/compile_typst.py <typ_file> [--output <output.pdf>]
```

**Example:**
```bash
python3 scripts/compile_typst.py resume_executive.typ
# Creates: resume_executive.pdf

# Or specify custom output name:
python3 scripts/compile_typst.py resume_executive.typ --output brent_skoumal_resume.pdf
```

Typst compiles in a single pass with no auxiliary files to clean up.

### YAML shape

There is no schema validator installed in this repo — a malformed `cv.yaml`
will fail at Jinja-render time with a Python traceback instead of a friendly
message. Check the file against `references/yaml-schema.md` before compiling
if the template output looks wrong or empty.

### Review PDF

After compilation:
1. **Visual review:** Check formatting, layout, spacing
2. **Content review:** Verify all sections rendered correctly
3. **ATS test:** Copy-paste text to ensure proper extraction
4. **Print test:** View in grayscale for B&W readability

### Iterate if Needed

1. Edit the YAML source (not Typst)
2. Regenerate Typst from updated YAML
3. Recompile to PDF
4. Review again

**Why edit YAML instead of Typst:**
- Easier to maintain and update
- Can regenerate with different templates
- `cv.yaml` stays traceable to `cv-tailor`'s output, keeping content and layout separately editable

## Prerequisites

### Python packages

```bash
pip install -r requirements.txt
```

Installs `pyyaml` and `jinja2`, the only two dependencies the scripts import.

### Typst Installation

**macOS:**
```bash
brew install typst
```

**Linux:**
```bash
# Via cargo (requires Rust)
cargo install typst-cli

# Or via package manager (check availability)
```

**Windows:**
```bash
winget install --id Typst.Typst
```

**Verify:**
```bash
typst --version
```

## Quick Customization

### Change Colors

Edit the color definitions at the top of the template:
```typst
#let primary = rgb("#1e3a5f")    // Header and section color
#let accent = rgb("#0369a1")     // Links, dates
```

### Change Font

All templates, near the top:
```typst
#set text(font: "Inter", size: 9pt)  // Change font name
```

Common alternatives: "Helvetica", "Arial", "Source Sans Pro", "Roboto"

### Change Margins

```typst
#set page(margin: (top: 0.4in, bottom: 0.35in, left: 0.5in, right: 0.5in))
```

## Tips for Best Results

**Content preparation:**
1. Get `cv.yaml` from the `cv-tailor` skill (Stage 5 writes it alongside `cv.md`) — see `references/yaml-schema.md` for the exact shape if writing one by hand
2. Keep resume to 1-2 pages
3. Use consistent date formatting
4. Ensure all required YAML fields present

**Template selection:**
1. Default to generating both Executive and Tech Modern (see "Default templates" above)
2. Compact if you have 10+ years of detailed experience and need more density
3. Minimal for creative/design-adjacent roles
4. Modern Dense only for content that genuinely needs 20-25 bullets on one page

**PDF generation:**
1. Always review PDF before submitting
2. Test text extraction (copy-paste from PDF)
3. Check both screen and print appearance
4. Keep source YAML for easy updates

**File naming:**
```
Good: firstname_lastname_resume.pdf
Good: firstname_lastname_companyname.pdf
Avoid: resume.pdf, cv_final_v3.pdf
```

## Complete Example

```bash
# Starting from YAML resume — default pair (Executive + Tech Modern):

python3 scripts/yaml_to_typst.py resume.yaml executive \
  --output resume_executive.typ
python3 scripts/compile_typst.py resume_executive.typ \
  --output final_resume_executive.pdf

python3 scripts/yaml_to_typst.py resume.yaml tech-modern \
  --output resume_tech-modern.typ
python3 scripts/compile_typst.py resume_tech-modern.typ \
  --output final_resume_tech-modern.pdf

# Review both
open final_resume_executive.pdf final_resume_tech-modern.pdf  # macOS
# or
xdg-open final_resume_executive.pdf  # Linux

# (Optional) Generate another template on request
python3 scripts/yaml_to_typst.py resume.yaml compact \
  --output resume_compact.typ
python3 scripts/compile_typst.py resume_compact.typ \
  --output final_resume_compact.pdf
```

## Integration with Other Skills

**Complete resume workflow in this repo:**

1. **Tailor:** `cv-tailor` runs the JD-matching pipeline and writes `cv.md` + `cv.yaml` into the job folder
2. **Format:** `resume-formatter` (this skill) converts `cv.yaml` to Typst and compiles the PDF
3. **Review:** `resume-reviewer` does visual QA on the compiled PDF
4. **Iterate:** Fix content in `cv.yaml` (or re-run cv-tailor stages), then regenerate

This keeps resume data in editable YAML format while producing professional PDF output.
