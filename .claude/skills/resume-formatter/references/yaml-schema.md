# Resume YAML schema

The fields every `*.typ.j2` template reads. All top-level sections except
`contact` are optional — omit a key entirely (don't leave it empty) to skip
that section in the rendered PDF.

```yaml
contact:
  name: str                # required
  title: str                # optional — role title under the name
  location: str             # optional
  phone: str                 # optional
  email: str                 # optional
  linkedin: str               # optional — bare handle/path, no "https://"
  github: str                 # optional — bare handle/path, no "https://"

summary: str                 # optional, 1-2 lines

experience:                  # optional, reverse chronological
  - company: str
    location: str            # optional
    positions:                # one company can have multiple positions (promotions)
      - title: str
        dates: str            # e.g. "Sep 2022 – Present"
        achievements:
          - str                # one bullet per line

skills:                      # optional — dict of category -> list of terms
  Category Name:
    - str

education:                   # optional
  - degree: str
    institution: str
    graduation_year: str

certifications:              # optional
  - name: str
    issuer: str
    date: str

projects:                    # optional
  - name: str
    dates: str                # optional
    technologies: [str]       # optional
    description: str          # optional
    achievements: [str]       # optional

publications:                # optional
  - authors: str
    title: str
    venue: str
    date: str
    url: str                  # optional

awards:                      # optional
  - name: str
    issuer: str
    date: str

languages:                   # optional
  - language: str
    proficiency: str

volunteer:                   # optional
  - role: str
    organization: str
    dates: str
    description: str          # optional
```

## Notes

- This maps directly onto `templates/cv-structure.md`'s skeleton: `contact` +
  `summary` = Header/Summary, `experience` = Experience, `skills` = Skills
  (keep to ≤3 categories per that skeleton), `education`/`certifications` as
  named, `projects` only when used.
- `skills` categories render in the order they appear in the YAML mapping.
- There is no schema validator installed in this repo (`yaml_to_typst.py`'s
  optional `from schema import validate_resume` import is a no-op here) — get
  the shape right by hand against this doc, or against `references/examples.md`.
