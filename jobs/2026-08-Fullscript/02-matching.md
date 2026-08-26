# Stage 2 — Matching & Gap Report: Fullscript, Senior Backend Engineer

**Note on profile.md**: visibility rules and preferences in `master/profile.md` are still template placeholders (no explicit include/exclude rules, date format, or region convention set). No content is being excluded on visibility grounds as a result — everything below is included purely on relevance to this JD. Flagging this so you can confirm before Stage 3, especially date format and whether to show your Yerevan location as-is for a role paying in CAD.

## Must-haves

| Requirement | Evidence in master CV | Confidence | Notes |
|---|---|---|---|
| Strong experience with Ruby or Ruby on Rails | None. All backend work is Python/Django, FastAPI, plus earlier Java/Spring Boot. | **None** | Hard gap — see below. |
| Designing maintainable systems, pragmatic tradeoffs | XML merge service redesign; reporting proxy service; ReAct loop rework (cut runtime deps 15→6, locked tree 66→45); `IToolHandler`/`IConversationStore` protocol design | High | Strong, well-evidenced. |
| Strong testing habits, tests support maintainability | 43-test suite (14 integration + 29 unit) added where none existed; flow/regression test automation at Synopsys (Perl/Tcl) | High | Direct match. |
| Platform, infrastructure, tooling, developer experience | Agentic assistant CI/CD + Helm/GitLab pipeline ownership; Docker multi-stage builds; Kubernetes/GKE delivery; standalone customer-side automation frameworks at Synopsys | High | Strong infra/tooling depth, cross-domain. |
| Desire to improve engineering standards across teams | SOLID principles meetup talk driving refactors; Python tutoring on clean architecture/OOP; ADR authorship and alignment | High | Well evidenced. |
| Strong communication, cross-team collaboration | Event Storming facilitation across R&D/product/design; ADR alignment across product/API/reporting teams; coordinated 10+ contributors across engineering/platform/ops/data science/product/PM | High | Strong. |
| Willingness to learn, ask questions, receive feedback | Reworked LangGraph prototype after validating framework limitations; knowledge-sharing sessions with platform/ops teams | Medium | Inferred from behavior, not stated directly as a trait. |
| Own long-term technical health of a monorepo | Nx monorepo tooling listed as skill; no direct "owned monorepo health" accomplishment | Low–Medium | Monorepo *exposure* exists, not clear ownership of one at this scale. |
| Plan solution designs & release strategies with stakeholders | ADR for reporting transition; design doc for agentic assistant end-to-end; staging/production promotion planning | High | Strong. |
| Lead foundational upgrades across the stack | Python 3.10→3.11 upgrade across two product areas; XML merge service redesign; auth/authorization refactor | High | Direct match, though language stack differs (Python not Ruby). |
| Improve code quality, application structure, maintainability | Clean architecture refactors driven from SOLID talk; reporting service restructuring for scalability/maintainability | High | Strong. |
| Address scalability, reliability, performance | Reporting aggregates rebuilt to cut UI load times; memory/time-consumption analysis for XML merging; connection reuse via shared async HTTP client | High | Strong, with concrete outcomes. |
| Resolve security vulnerabilities | Auth/authorization refactor resolving missing user-update behavior; vault-sourced secrets in Helm deploy | Medium | Adjacent (auth correctness, secrets handling) rather than explicit vuln remediation. |
| Build/maintain developer tooling, CI linting, QoL improvements | Authored GitLab CI/CD pipeline and Helm values (template validation, staging/prod deploy, rollback jobs); standalone Python automation framework at Synopsys | High | Strong, direct CI/tooling ownership. |
| Maintain shared infra: feature flags, e2e tests, IaC, within a monolith | Feature-flag modernization: ~800 flags / 4,000 config rows generated, naming validation implemented; Helm/GitLab CI as IaC-adjacent delivery | Medium–High | Feature-flag work is a strong, literal match. |
| Support product teams via cross-cutting technical issues | Reporting proxy service unblocking multiple product teams; reverse proxy proposal resolving platform-migration bottleneck | High | Strong. |
| Act as a multiplier, unblock other teams | Knowledge-sharing sessions; mentoring two interns promoted within a year; engineering-lead role over 6+ engineers | High | Strong. |
| Implementation, code review, technical guidance, mentorship, documentation | Mentored interns (Synopsys); Python tutoring (Criteo); ADR/documentation authorship throughout | High | Strong. |

## Nice-to-haves

| Requirement | Evidence in master CV | Confidence | Notes |
|---|---|---|---|
| Scaling / high-scale web applications | Criteo is large-scale AdTech; reporting/data-platform work at scale implied but no explicit traffic/scale metrics in master CV | Medium | Framing opportunity, not a hard number to cite. |
| E-commerce or health tech sector | None — AdTech, fintech, semiconductor, EdTech (teaching) | **None** | Genuine gap. |
| React or GraphQL | React/Ant Design admin dashboard (PEI Development); Angular elsewhere; GraphQL — none | Medium | React evidenced; GraphQL is a gap. |
| Improving CI systems, test suites, feature flags, developer tooling | GitLab CI/CD pipeline authorship; 43-test suite; feature-flag modernization (~800 flags) | High | Strong match. |

## Gaps

- **Ruby / Ruby on Rails — no evidence at all.** This is the JD's single explicit hard requirement and the master CV has zero Ruby experience (Python/Django/FastAPI and Java/Spring Boot instead). This cannot be honestly covered. Recommend the CV lean on directly transferable backend-framework depth (Django/DRF, FastAPI, Spring Boot — all MVC-style, ORM-backed web frameworks) and let the summary state the language gap plainly as fast-ramp potential rather than implying Rails experience. **This is a significant risk for this application regardless of CV framing — worth a candid conversation before investing further in tailoring.**
- **E-commerce or health tech sector** — no direct experience (AdTech, fintech, semiconductor, EdTech). Nice-to-have only; omit rather than stretch.
- **GraphQL** — no evidence. Omit; do not list under Skills.
- **Explicit high-scale metrics** (req/sec, data volume, uptime SLAs) — scale is implied by employer (Criteo, Synopsys enterprise customers) but no hard numbers are recorded in the master CV to cite truthfully.
- **Monorepo ownership at scale** — Nx monorepo is listed as a tool touched, not something owned long-term; won't claim "owned monorepo health."

## Excluded content

- Quality Assurance Engineer role (Synopsys, 2016–2019) — older role (~10 years), lower relevance to backend/platform engineering; condense to a single line or omit per length rules rather than a full entry.
- Fintech full-stack role's UI/frontend-heavy details (Ant Design UI specifics) — kept only insofar as they support React evidence for the nice-to-have; full admin-dashboard build detail is de-emphasized as not backend-infrastructure-relevant.
- PhD/electronics education and lecturer role — included briefly (Education section, one line) but de-emphasized in Experience narrative; not relevant to backend infrastructure engineering beyond signaling mentorship/teaching ability, which is already evidenced elsewhere.
- Kinetic Wall side project — unrelated to backend/platform infrastructure theme; omit from a 1–2 page tailored CV in favor of Agentic Troubleshooting Assistant project entry.
- Yield Explorer / semiconductor tooling deep technical detail (Bin/Wafer analysis specifics) — kept as condensed single-line evidence of automation-framework and tooling work; deep domain detail excluded as irrelevant to Rails/web backend context.

---

**Before proceeding to Stage 3**, please confirm:
1. You're aware the Ruby/Rails requirement is a hard, unaddressed gap — do you still want a tailored CV for this role?
2. OK with profile.md defaults (no exclusions, 1-page target, no stated date/region format) until you fill that file in?
