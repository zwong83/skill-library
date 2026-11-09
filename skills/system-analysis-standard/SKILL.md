---
name: system-analysis-standard
description: Create or audit visual-first, implementation-oriented System Analysis documents with system-level and per-feature As-Is, problem, To-Be, state, data, and integration views while preserving the boundary between logical analysis and technical design.
---

# Standard System Analysis

Use this skill when the user wants to create, refine, compare, or quality-check a System Analysis document. The output explains how the required system behavior is decomposed and allocated at a logical level so that technical design can begin from a consistent analysis baseline.

This skill governs the System Analysis artifact. Invoke conditional companion skills only where this standard directs; they provide focused analysis guidance without replacing SA ownership.

## Core operating rules

- Treat supplied requirements, source documents, confirmed decisions, and approved constraints as the source of truth.
- Read identified source material completely before analyzing it.
- Never invent business scope, actors, policies, data ownership, service boundaries, performance targets, security requirements, technology choices, or approvals.
- Label uncertainty as `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Pending Approval`, `Open`, or `Deferred`.
- Separate logical analysis from technical design. Describe responsibilities, behavior, boundaries, flows, and decisions; leave framework, deployment, class, schema, and protocol choices to System Design.
- Do not silently resolve contradictions. Record the conflict, impact, decision owner, and required resolution.
- Use stable IDs and maintain traceability from source requirements through analysis decisions and verification scenarios.
- Invoke/read `software-security-standard` in System Analysis mode when protected assets, identities, permissions, trust boundaries, sensitive data, abuse, privacy, compliance, or security risk are applicable. Identify requirements and unresolved policy decisions without choosing cryptographic algorithms, identity products, key platforms, or other implementation mechanisms.

## Visual-first and per-feature diagram policy

Use diagrams as the primary representation for the system and for every in-scope feature. Read [references/feature-diagram-coverage.md](references/feature-diagram-coverage.md) for every full draft or review. A full SA must show the main flow, current system logic and problems for brownfield scope, target solution logic, conceptual data model, and a dedicated To-Be logical-flow diagram for every feature.

- Invoke/read `plantuml-syntax` before creating or modifying PlantUML and load only the relevant reference.
- Use one focused diagram per question; do not combine unrelated concerns into an unreadable diagram.
- Keep prose short. Use text and compact tables only for rules, constraints, assumptions, exceptions, decisions, acceptance criteria, traceability, and unresolved items that the visual cannot state precisely.
- Every diagram must have a title, scope, textual explanation, source traceability, and any necessary legend or assumptions.
- If a diagram and text conflict, the explicit text or Decision Register governs and the conflict must be fixed before approval.
- A table may replace a conditional supporting diagram, but it may not replace the system main-flow views or the dedicated To-Be technical-logic diagram required for each feature.

## Input classification

### Mandatory inputs

- Task mode: draft, refine, compare, or review.
- System/product/feature identity and target release/scope when known.
- A complete requirements baseline for new analysis: at least an SRS, PRD, BRD, or equivalent accepted requirements statement.
- The complete existing System Analysis for refinement or review.

### Conditional inputs

- Where detailed feature behavior affects the analysis, require the governing FRS or an authorized equivalent requirements baseline with testable behavior and acceptance. Record its scope and authority; absence of a separate FRS is not a waiver.
- A Change Request is mandatory for change-focused analysis, but not for greenfield analysis.
- Security/privacy, performance, integration, data-retention, availability, recovery, and operational constraints are mandatory when applicable; if not applicable, record `Not Applicable`.
- PRD, BRD, SRS, approved technical constraints, and integration decisions are mandatory when the analysis decision depends on them.

### Optional context

- Research, screenshots, examples, diagrams, logs, benchmarks, and preferred notation are optional unless a requested decision depends on them.

## Source and readiness gate

1. Classify the task as drafting, refining, comparing, or reviewing System Analysis.
2. Identify the governing requirements and record their title, version/date, status, and location when available.
3. Read the source material completely and extract scope, actors, business rules, functional behavior, NFR implications, integrations, data sensitivity, and unresolved decisions.
4. If source material is missing or materially ambiguous, ask for it or clearly mark the analysis as limited and not design-ready.
5. Block a design-ready conclusion when material scope, ownership, state, integration, security, or acceptance decisions remain unresolved.

## Workflow

1. Read [references/system-analysis-template.md](references/system-analysis-template.md) and [references/feature-diagram-coverage.md](references/feature-diagram-coverage.md) for a full draft or structural review.
2. Establish the system context, boundaries, actors, capabilities, external dependencies, and assumptions.
3. Build the feature inventory, upstream feature-point reconciliation, and diagram coverage matrix. Classify each feature as `New`, `Contract`, `Logic`, `Deleted`, or `No Change`, including reuse/defer/other-domain disposition. For brownfield scope, identify evidence for the As-Is system and problem IDs before proposing To-Be behavior.
   - Reconcile the individual actor/system operations under each feature against the approved requirements. Use the [shared functional coverage method](../prd-standard/references/functional-coverage.md) when available. Map each in-scope action to its logical owner, state/guard, normal and material failure path, and verification. Report omissions independently of diagram count.
4. Decompose requirements into use cases, system responsibilities, logical components, domain concepts, states, workflows, and cross-cutting concerns. When security is applicable, identify assets, actors/workload identities, trust boundaries, sensitive data, abuse cases, permission needs, and security acceptance outcomes.
5. Create system-level As-Is/problem/To-Be views and a dedicated To-Be technical-logic view for every feature. Analyze preconditions, main path, alternate path, failure path, authorization, idempotency, concurrency, recovery, audit, and observable outcomes.
6. Define conceptual/logical data models, ownership, lifecycle, logical create/read/update/delete/publish behavior, consistency needs, retention/access implications, and source-of-truth responsibilities without writing physical schemas, DDL, or concrete DML.
7. Define integration and middleware capability needs at a logical level without selecting products, topology, cache keys, topics/queues, endpoint contracts, or protocol designs.
8. Record analysis decisions, rationale, impacts, risks, dependencies, and unresolved questions.
9. Maintain traceability:

   `Source requirement -> Analysis capability/use case -> Logical responsibility/flow -> Design input -> Verification scenario`

10. Run [references/quality-gate.md](references/quality-gate.md) before delivery.

## Analysis artifact boundaries

System Analysis may include:

- context and scope boundaries;
- actor and responsibility allocation;
- capability decomposition;
- use cases and logical workflows;
- state models and transition rules;
- logical data ownership and lifecycle;
- integration purpose and business-level exchange;
- cross-cutting security, reliability, observability, and recovery concerns;
- decision rationale and impacts, risks, dependencies, and open decisions.

Keep these out of System Analysis unless the user explicitly requests a combined artifact:

- framework, language, package, class, or module choices;
- physical database tables, indexes, DDL, and migration scripts;
- endpoint paths, payload schemas, protocol details, and infrastructure topology;
- detailed algorithms, code, deployment manifests, or operational commands.

## Requirement and analysis writing standard

Use stable IDs such as `SA-CTX-001`, `UC-ORD-001`, `FLOW-CHK-001`, `DATA-001`, `INT-001`, and `DEC-001`.

Each analysis statement should identify the source requirement, logical subject, responsibility, behavior or decision, status, and downstream design or verification impact. Use the mandatory system/per-feature diagrams for technical logic and concise text only for exact meaning the visuals cannot safely carry.

## Deliverable conventions

- Use PlantUML diagrams as the primary navigation and explanation, with short Markdown tables/bullets as the normative supplement.
- Include the feature/diagram coverage matrix and do not claim design readiness while an in-scope feature lacks its required visual logic.
- Preserve section numbering when refining an existing analysis.
- Include source traceability, assumptions, risks, open decisions, review status, and version history.
- When no destination is specified, use `output/SA/SA-<project-name>.md`.
- Keep reusable PlantUML sources under `output/SA/diagrams/` and link them by diagram ID. When rendering support exists, generate and embed SVG/PNG previews while retaining the `.puml` source; do not claim syntax/render validation unless it was executed.
- Do not call the analysis approved or design-ready while material decisions, ownership, or source requirements remain unresolved.
