# Master CV — Hrachya Gumroyan

<!-- This file is your single source of truth. It is meant to be TOO LONG.
     Write everything: every role, project, metric, tool, talk, side project.
     Nothing here goes to an employer directly — the pipeline selects from it.
     Keep the structure below consistent; Stage 2 matching depends on it. -->

## Contact
- Name: Hrachya Gumroyan
- Email: hrgumroyan@gmail.com
- Phone: +374 (95) 122123
- Location: Yerevan, Armenia
- LinkedIn / GitHub / Website: <TODO — add LinkedIn URL, GitHub handle, personal site if any>

## Professional Summary
Software Development Engineer with 10 years of experience across backend engineering, API design, platform modernization, test automation, and technical leadership. Strongest technical focus is Python/Django backend development, REST APIs, PostgreSQL-backed systems, reporting/data flows, observability, and service architecture. Experienced in owning ambiguous cross-team initiatives from design and architecture discussions through implementation, production validation, documentation, and stakeholder alignment. Recognized in 2026 as an engineering lead for a feature team of 6+ engineers working with 2 product managers across reporting, billing, agentic troubleshooting, and platform decoupling work. Designed and shipped a production LLM agent (Python/FastAPI, Azure OpenAI, custom ReAct loop) to Kubernetes, including its Helm and GitLab CI/CD delivery path. Brings additional depth from Java/Spring Boot fintech development, semiconductor yield-analysis tooling, QA automation, and teaching.

## Skills Inventory
<!-- Full keyword surface. Role-level "Skills/tools used" lines below are the per-job slice of this. -->

**Languages:** Python, Java, JavaScript, Perl, Bash, Lua, Tcl, SQL

**Frameworks & libraries:** Django, Django REST Framework, FastAPI, Spring Boot, ReactJS, Angular, MUI, Ant Design, Pydantic, httpx, pytest, NumPy, OpenCV

**Backend engineering:** REST API design and implementation, API proxying, backend filtering, export flows, service integration, XML processing, RNG schema validation, runtime correctness checks, data model design, validation and authorization logic

**Databases & data processing:** PostgreSQL, relational database design, XML, RNG schema validation, ETL pipelines, reporting aggregates, data export flows, performance-oriented aggregation, currency conversion flows

**AI & LLM engineering:** Azure OpenAI, LLM tool/function calling, JSON-schema structured outputs, ReAct agent loops, agentic assistant design and production rollout, prompt engineering for deterministic scenario-based diagnostics, tool-handler protocol design, pluggable extension surfaces, LangGraph/LangChain (evaluated and replaced), Langfuse tracing and feedback scoring, async Python services for LLM workloads

**Architecture & system design:** Architecture Decision Records, C4 modeling, Domain-Driven Design, Event Storming facilitation, service decoupling and modernization, authentication/authorization refactoring, reverse proxy and migration planning, SOLID principles, clean architecture, object-oriented design, design patterns, technical design documents

**Cloud, infrastructure & delivery:** AWS S3, AWS EC2, Docker and multi-stage builds, Kubernetes (GKE), Helm charts and per-environment values, GitLab CI/CD, staging/production promotion, deployment validation and rollback jobs, Nx monorepo tooling, Linux, on-premises application environments

**Monitoring, observability & quality:** Prometheus, Grafana, Langfuse, integration testing, unit testing, production validation, test automation, request tracking, API metrics

**Leadership & ways of working:** Feature-team engineering leadership, quarterly OKR and capacity planning, cross-team dependency management, product/engineering stakeholder alignment, technical risk identification, scope negotiation, mentoring, tutoring, knowledge sharing, API documentation

## Experience

### Software Development Engineer — Criteo — Yerevan, Armenia
**Sep 2022 – Present**
Context: AdTech engineering role across backend systems, reporting APIs, platform modernization, product delivery, and architecture design. Recognized in Q2 2026 as engineering lead for a feature team of 6+ engineers partnering with 2 product managers, covering reporting, billing/pricing, agentic troubleshooting, and platform decoupling initiatives. Works hybrid (office/remote) within a globally distributed team with no local peers, collaborating daily across time zones.

Accomplishments (one per line, with real numbers wherever you have them):

*Technical leadership and planning*
- Formally recognized in Q2 2026 as engineering lead for a feature team of 6+ engineers, partnering with 2 product managers across reporting, billing/pricing, agentic troubleshooting, and platform decoupling initiatives.
- Owned the team's quarterly OKR and capacity plan, including initial scope allocation and rebalancing as priorities shifted during the quarter.
- Coordinated delivery across multiple teams and systems, managing dependencies, clarifying scope, and keeping timelines realistic for multi-quarter initiatives.
- Acted as engineering contact point for a blocker-priority pricing change, organizing clarification sessions around pricing logic and schema changes before implementation.
- Handled team meetings and quarterly planning sessions during the feature-team lead's absence, preserving delivery continuity and team alignment.
- Initiated internal Python tutoring sessions covering Python fundamentals, object-oriented programming, clean architecture, and design patterns through practical live coding.
- Presented SOLID principles during a team technical meetup and drove improvements to poorly structured code using clean architecture practices.

*AI and agentic systems*
- Led design and implementation of the first agentic troubleshooting assistant in the product area, owning the initiative end to end from kickoff and design document through proof of concept, backend implementation, and staging/production rollout on Kubernetes.
- Built the service as an async Python/FastAPI application backed by Azure OpenAI, exposing a diagnosis endpoint, a user-feedback endpoint, and health checks behind forwarded-token authentication, with dependencies wired through the FastAPI lifespan.
- Authored the architecture combining deterministic diagnostics with LLM-based explanations: scenario-based orchestration across five delivery states (inactive, no delivery, low delivery, live delivery, insufficient data), explicit classification rules, and Langfuse-based observability.
- Coordinated work across 10+ contributors from engineering, agentic platform, operations, data science, product, and program management, delivering a working prototype on schedule despite ambiguous scope and cross-team dependencies.
- Reworked the initial LangGraph state-graph prototype into a custom ReAct loop after validating framework limitations — cutting direct runtime dependencies from 15 to 6 and the locked dependency tree from 66 to 45 packages, and removing a framework abstraction layer that made agent behaviour hard to trace, test, and reason about.
- Designed the tool layer around a small `IToolHandler` protocol where each of the 7 diagnostic tools co-locates its name, JSON schema, and async execution, and documented an extension model that keeps new tools behind a well-defined integration surface without touching the agent loop.
- Constrained model output using Azure OpenAI JSON-schema structured outputs to separate chain-of-thought from the user-facing report, with graceful fallback parsing so a non-conforming response never breaks the loop.
- Wrote the ~600-line system prompt as an explicit diagnostic contract: per-tool field semantics, ordered stop-at-first-match decision rules, tool call-ordering constraints, scope guardrails, and the structured Markdown report format returned to CSMs and curators.
- Implemented per-request bearer-token propagation to internal APIs and a single shared async HTTP client for connection reuse across all tool calls, keeping one agent instance safe to serve concurrent users.
- Built conversation memory behind an `IConversationStore` protocol with a bounded in-memory implementation (O(1) eviction), keeping the persistence backend swappable without changing the agent.
- Instrumented each run as a full Langfuse trace tree (run span, per-iteration LLM generations, per-tool spans with error levels) and returned trace IDs to the client, so end-user thumbs-up/down ratings, categories, and comments are written back as scores against the exact run that produced them.
- Added a 43-test suite (14 integration scenario tests plus 29 unit tests) where the earlier prototype had none, improving confidence in the agent workflow and aligning the Python implementation with the planned C# migration contract.
- Packaged the service as a multi-stage Docker image against internal registry and PyPI mirrors and shipped it to GKE via Helm, with vault-sourced secrets, ingress path routing, and per-environment model, endpoint, and replica configuration for staging and production.
- Owned the agent's CI/CD and deployment setup inside Criteo's existing GitLab CI platform framework: authored the application's pipeline definition and Helm values covering template validation, staging and production deploys, revision checks, and rollback jobs, and drove image promotion through to the production release.
- Drove knowledge-sharing sessions with platform and operations teams to transfer context, gather feedback, and make the agent architecture understandable beyond the immediate implementation team.

*Reporting APIs and data platform modernization*
- Drove the initiative to replace dependency on a deprecated reporting source by proposing an isolated reporting proxy service that could retrieve consolidated reporting data, support future manipulation, and scale independently.
- Authored and aligned an Architecture Decision Record for the reporting data transition, gathering feedback from product, API, and reporting teams to remove weak points before implementation.
- Developed reporting APIs integrating multiple data endpoints, applying backend filtering, exposing performance-related data, and supporting frontend changes for the new reporting flow.
- Created reusable reporting API endpoints and export flows, restructuring the reporting integration service to improve scalability, maintainability, and separation between UI and API responsibilities.
- Built smaller reporting aggregates for the UI to reduce load times, coordinated the ETL release, and validated correctness of the new aggregates in the product reporting experience.
- Extended Prometheus/Grafana metrics for reporting integrations and built a dedicated Grafana dashboard later transferred to the team's monitoring space.
- Improved request traceability by adding user identifiers to API calls and updating backend/configuration paths to support better monitoring and troubleshooting.
- Refactored proxy contracts and separated UI/API endpoints to improve control, traceability, and monitoring of reporting flows.
- Contributed backend/API work to a shared reporting modernization outcome that improved customer perception of reporting.
- Produced documentation for the transition from the deprecated reporting API to the new product API, which later supported public-facing reporting API documentation.

*Architecture, modernization, and reliability*
- Led and implemented core parts of an XML merge initiative, including runtime RNG validation for production XML merge jobs, scalable service refactoring, and updates to Lua-side schema entities.
- Designed and implemented a separate XML merge service to download, merge, and validate XML outputs, simplifying technical architecture and improving maintainability.
- Conducted memory and time-consumption analysis for XML merging to assess performance characteristics and support future scalability decisions.
- Participated in platform convergence and on-premises migration work as a technical point of contact, using phased-migration precedent and estimation risk to argue successfully for reducing first-phase scope.
- Identified a potential interconnect bottleneck during platform migration planning, proposed a reverse proxy approach, and engaged the security team to move the discussion toward an actionable solution.
- Researched and refactored authentication mechanisms across product areas in collaboration with API and external teams, resolving missing user-update behavior after authentication changes.
- Contributed to authorization and feature-flag modernization by analyzing the permission model, generating configuration for approximately 800 feature flags and 4,000 configuration rows, documenting the approach, and implementing naming validation.
- Upgraded backend codebases from Python 3.10 to Python 3.11 across two product areas, supporting runtime modernization and long-term maintainability.
- Handled production investigations and drove resolution of a core deal-mechanism issue in collaboration with relevant stakeholders.

*Product delivery and cross-team collaboration*
- Led implementation of a product update allowing simultaneous app and web inventory selection in supply packages, aligning requirements with product stakeholders and sharing domain knowledge with the team.
- Enhanced audience/data segment management flows, including API and database updates, management restrictions, and processing-issue resolution to separate product business processes more clearly.
- Designed and implemented the data model, REST APIs, initial UI, validation, and authorization for SRM mapping functionality, then added XML export endpoints for integration and operational needs.
- Researched currency-conversion options across product, billing, and reporting systems; drafted a backend-side conversion service before the final architecture moved conversion to the data source, then ensured correct API/UI behavior including edge cases.
- Facilitated cross-team Event Storming sessions based on Domain-Driven Design principles to build a shared domain model and improve understanding between R&D, product, design, and engineering stakeholders.
- Participated in cross-functional Q&A and retrospective sessions to improve process transparency and consolidate architecture/domain-modeling insights.
- Delivered backend and frontend work against a fixed marketing deadline without significant production issues, while coordinating with product and partner teams as details evolved.
- Contributed beyond the primary backend stack through Lua, Angular, and frontend changes, supporting cross-stack delivery and stronger product-level ownership.

Skills/tools used: Python, Django, Django REST Framework, FastAPI, Pydantic, httpx, pytest, PostgreSQL, REST API design, Azure OpenAI, LLM tool/function calling, JSON-schema structured outputs, ReAct agent loops, prompt engineering, LangGraph/LangChain, Langfuse, Docker, multi-stage builds, Kubernetes, GKE, Helm, GitLab CI/CD, Prometheus, Grafana, XML, RNG schema validation, ETL, Lua, Angular, JavaScript, Nx monorepo, Architecture Decision Records, C4 modeling, Domain-Driven Design, Event Storming, SOLID, clean architecture, reverse proxy design, feature flags, authentication/authorization, technical leadership, OKR planning, mentoring.

### Full-Stack Engineer — Steven / PEI Development — Yerevan, Armenia
**Sep 2021 – Sep 2022**
Context: Early-stage FinTech startup building a consumer mobile app for splitting and sharing bills among friends (a simpler, Splitwise-style expense-sharing product), later extended with a branded Mastercard for premium users — loadable and usable for in-app transactions — with integrations spanning BankID, Swish, IBAN, and Apple Pay. Team of five (two backend, one admin developer, one iOS, plus myself); owned the internal admin platform and contributed to backend maintenance.

Accomplishments (one per line, with real numbers wherever you have them):
- Owned the operations admin dashboard end to end — React / Ant Design front-end and Java / Spring Boot backend — used internally to manage user groups, perform account and group adjustments per user requests, and support customer-service workflows.
- Inherited an existing admin platform on joining and took over its maintenance and evolution, shipping changes and new capabilities as product and support needs emerged.
- Designed and built a keyword-triggered promotions feature end to end (admin UI + Spring Boot backend): an internal system that surfaced partner promotions to users when specific keywords appeared in group descriptions or logged expenses — a lightweight, vendor-independent alternative to integrating a third-party ad network. Shipped to production, serving ~17–20 active partner promotions.
- Contributed to general backend maintenance across the product in Java / Spring Boot, supporting the two core backend engineers and keeping internal tooling aligned with evolving product needs.
- Built and served promotion assets from AWS S3 and worked with services deployed on AWS EC2 (consumed existing cloud infrastructure rather than provisioning it).
- Worked in a fintech product context spanning card issuance (Mastercard), BankID, Swish, IBAN, and Apple Pay integrations.

Skills/tools used: Java, Spring Boot, React, Ant Design, JavaScript, REST APIs, AWS S3, AWS EC2, admin tooling, fintech integrations (Mastercard, BankID, Swish, IBAN, Apple Pay), full-stack development.

### Application Engineer — Synopsys Armenia — Yerevan, Armenia
**Jan 2019 – Sep 2021**
Context: Customer-facing application engineering on Yield Explorer, Synopsys' yield-management and volume-diagnostics platform, supporting advanced-node yield analysis for major semiconductor customers including Qualcomm and Intel. Bridged R&D, field teams, and customer engineering to build customer-specific analysis applications, evaluate tooling readiness for advanced process nodes, and drive adoption at the customer site.

Accomplishments (one per line, with real numbers wherever you have them):

*Advanced-node investigation and customer adoption (Qualcomm)*
- Led evaluation of Yield Explorer's ability to handle the data volumes and failure mechanisms of 5nm and 3nm process nodes, including benchmarking and methodology validation for test-chip failure analysis.
- Reverse-engineered a customer's test-chip failure-analysis methodology — previously implemented only in Excel — and rebuilt it as a native Yield Explorer application using built-in tooling, custom macros, and Bash-driven analysis flows.
- Discovered during development that the customer's existing Excel-based calculations were fundamentally incorrect and did not reflect physical reality; validated the discrepancy against the corrected implementation.
- Presented the findings directly to the customer's VP of Yield Analysis, demonstrating the new application and walking through the specific points where their established calculations were wrong.
- Won customer adoption of the new application as a result, driving additional Yield Explorer license consumption and replacing the flawed Excel-based process with a validated in-tool workflow.

*Customer-specific YMS applications*
- Built customer-centered analysis applications delivering Bin, Wafer, and broader YMS-oriented analysis, including test-chip data analysis, Bin Analysis, Wafer Analysis, and defect/pattern detection.
- Developed custom analysis utilities for data manipulation and adjustment to enable correct visualization within Yield Explorer, alongside standard YMS analysis visualizations.

*Field integration and on-premises deployment (Intel)*
- Supported Intel over ~2 years in integrating Synopsys yield tooling with their internal data pipeline, adapting custom YMS analysis tools to Intel's data model and writing middleware scripts to transform their data into the Yield Explorer schema.
- Developed newly requested analyses on Intel's datasets, extending the tooling to meet evolving customer requirements.
- Designed and deployed a pure-Python, dependency-free semi-automation framework that ran on locked-down customer servers (no external library installation permitted), replacing a 100%-manual new-release verification process with a semi-automated one at customer sites.
- Architected the framework to launch Yield Explorer and execute preconfigured analyses end to end; where functionality lacked command-line support, designed a human-in-the-loop "operator" model to handle GUI pop-ups and selectors mid-flow, keeping otherwise un-automatable paths under test.

*Technical environment*
- Analyzed yield and test data from advanced-node (5nm/3nm) silicon; did not work directly in design flows.
- Worked with Python, Perl, Bash, Tcl, and Linux in production-adjacent, on-premises customer environments.

Skills/tools used: Python, Perl, Bash, Tcl, Linux, Yield Explorer, yield management systems (YMS), volume diagnostics, test-chip failure analysis, Bin Analysis, Wafer Analysis, defect/pattern detection, data transformation middleware, on-premises deployment, automation frameworks, customer-facing technical presentations.

### Quality Assurance Engineer — Synopsys Armenia — Yerevan, Armenia
**Jun 2016 – Jan 2019**
Context: Quality engineering on Yield Explorer, Synopsys' volume-diagnostics and yield-management platform used by leading semiconductor foundries to identify systematic failure mechanisms and accelerate yield ramp on advanced process nodes. Focused on flow-based test automation, cross-functional defect diagnosis, and informal team leadership within the Yield Management System (YMS) domain.

Accomplishments (one per line, with real numbers wherever you have them):
- Became the driving engineer for the YMS Analysis domain — one of four core domains of Yield Explorer — owning flow tests that replicated real customer analysis workflows to validate regression stability across releases.
- Developed automated regression and flow tests in Perl, with test scenarios authored as Tcl macros executed inside Yield Explorer's embedded scripting environment, exercising the product the way foundry engineers used it in production.
- Designed and deployed a standalone customer-side automation framework in pure Python, replacing a 100% manual new-release verification process with a semi-automated one and reducing hands-on verification effort at customer sites.
- Kept the framework deliberately dependency-free so it could run on locked-down foundry servers where installing external libraries was not permitted, and deployed it directly into customer-site release-validation workflows.
- Architected the framework to launch Yield Explorer and execute preconfigured analyses end to end; where product functionality lacked command-line support, partnered with Application Engineers to design a human-in-the-loop "operator" model that handled GUI pop-ups and selectors mid-flow, keeping otherwise un-automatable paths under test.
- Took personal ownership of two interns with no formal mandate, ramping them on the tooling and the yield-management domain; both were promoted from intern to mid-level engineer within roughly a year under my day-to-day guidance.
- Partnered continuously with developers, Application Engineers, and occasionally customers to review test status, reproduce field issues, and feed findings back into the product.

Skills/tools used: Perl, Python, Tcl, Bash, Linux, test automation, regression testing, flow-based testing, defect diagnosis, release validation, mentoring.

### Part-Time Lecturer — Yerevan State University, National Polytechnic University of Armenia, ACA — Yerevan, Armenia
**Sep 2019 – Present**
Context: Teaching introductory programming and digital circuit design automation to undergraduate students across three institutions, alongside a full-time engineering career.

Accomplishments (one per line, with real numbers wherever you have them):
- Delivered introductory Python courses and digital circuit design automation classes.
- Designed practical, project-based sessions for beginners and sophomore students.
- Combined software engineering and electronics experience to teach both programming fundamentals and applied automation concepts.

Skills/tools used: Python, teaching, curriculum design, digital circuit design automation, electronics, public speaking, mentoring.

## Projects (side projects, open source, freelance)

### Kinetic Wall
- Dynamic mechanical kinetic wall that tracks user movement and plays preloaded videos. Built the Python-based desktop application and backend service for kinetic-wall automation, plus an in-progress web application to improve accessibility and control. Tech: Python, FastAPI, NumPy, OpenCV.

### Agentic Troubleshooting Assistant (Criteo — internal product initiative)
- First agentic troubleshooting assistant in the product area; owned end to end from design document to production on GKE. Async Python/FastAPI service over Azure OpenAI with a custom ReAct loop, 7 diagnostic tools behind an `IToolHandler` protocol, JSON-schema structured outputs, Langfuse tracing and feedback scoring, 43-test suite, Docker/Helm/GitLab CI delivery. 10+ contributors coordinated across engineering, platform, operations, data science, product, and program management.

## Education
- PhD in Electronics, Micro- and Nanoelectronics, National Polytechnic University of Armenia, 2019–2022 (Yerevan, Armenia)
- 2013-2017 - Bachelor's degree - Electrical Engineering, National Polytechnic University of Armenia
- 2017-2019 - Master's degree - Electrical Engineering, National Polytechnic University of Armenia
- 2019-2022 - PhD - Electronics, micro- and nanoelectronics, National Polytechnic University of Armenia

## Certifications & Training
- TOEFL iBT — score 102 (ETS)
- <TODO — add any cloud, Kubernetes, or AI/LLM certifications, internal Criteo training, courses>

## Talks, Publications, Community
- Presented SOLID principles at an internal team technical meetup at Criteo, driving refactoring of poorly structured code toward clean architecture.
- Initiated and ran internal Python tutoring sessions at Criteo covering Python fundamentals, OOP, clean architecture, and design patterns through live coding.
- Ran knowledge-sharing sessions with platform and operations teams on the agentic troubleshooting assistant's architecture.
- Facilitated cross-team Event Storming sessions (Domain-Driven Design) with R&D, product, design, and engineering stakeholders.
- Part-time university lecturer since 2019 (Yerevan State University, National Polytechnic University of Armenia, ACA) — introductory Python and digital circuit design automation.
- Mentored two interns at Synopsys with no formal mandate; both promoted from intern to mid-level engineer within roughly a year.
- <TODO — add PhD-related publications, conference papers, or public talks if any>

## Languages
- Armenian — Native
- Russian — Near-native
- English — Advanced (TOEFL iBT 102)