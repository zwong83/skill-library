---
name: system-analysis-standard
description: Create or audit implementation-oriented system analysis documents that decompose approved requirements into system boundaries, actors, use cases, logical flows, responsibilities, data behavior, integrations, risks, and open decisions without becoming a detailed technical design.
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

## Diagram-first policy

Use diagrams as the primary representation when the analysis explains relationships, boundaries, flows, hierarchy, state, timing, or ownership. Prefer context, use-case, activity, state, logical class/domain, logical ER, and high-level sequence diagrams.

- Invoke/read `plantuml-syntax` before creating or modifying PlantUML and load only the relevant reference.
- Use one focused diagram per question; do not combine unrelated concerns into an unreadable diagram.
- Keep text as the authoritative source for rules, constraints, assumptions, exceptions, decisions, acceptance criteria, and unresolved items.
- Every diagram must have a title, scope, textual explanation, source traceability, and any necessary legend or assumptions.
- If a diagram and text conflict, the explicit text or Decision Register governs and the conflict must be fixed before approval.
- Do not add a diagram when a table or short paragraph communicates the relationship more clearly.

## Input classification

### Mandatory inputs

- Task mode: draft, refine, compare, or review.
- System/product/feature identity and target release/scope when known.
- A complete requirements baseline for new analysis: at least an SRS, PRD, BRD, or equivalent accepted requirements statement.
- The complete existing System Analysis for refinement or review.

### Conditional inputs

- FRS is mandatory when detailed feature behavior affects the analysis; otherwise record the limitation.
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

1. Read [references/system-analysis-template.md](references/system-analysis-template.md) for a full draft or structural review.
2. Establish the system context, boundaries, actors, capabilities, external dependencies, and assumptions.
3. Decompose requirements into use cases, system responsibilities, logical components, domain concepts, states, workflows, and cross-cutting concerns. When security is applicable, identify assets, actors/workload identities, trust boundaries, sensitive data, abuse cases, permission needs, and security acceptance outcomes.
4. Analyze each important flow for preconditions, main path, alternate path, failure path, authorization, idempotency, concurrency, recovery, audit, and observable outcomes.
5. Define logical data ownership, lifecycle, consistency needs, retention/access implications, and source-of-truth responsibilities without writing physical schemas.
6. Define integration responsibilities and business-level data exchange without writing endpoint contracts or protocol designs.
7. Record analysis decisions, alternatives, risks, dependencies, and unresolved questions.
8. Maintain traceability:

   `Source requirement -> Analysis capability/use case -> Logical responsibility/flow -> Design input -> Verification scenario`

9. Run [references/quality-gate.md](references/quality-gate.md) before delivery.

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
- alternatives, trade-offs, risks, dependencies, and open decisions.

Keep these out of System Analysis unless the user explicitly requests a combined artifact:

- framework, language, package, class, or module choices;
- physical database tables, indexes, DDL, and migration scripts;
- endpoint paths, payload schemas, protocol details, and infrastructure topology;
- detailed algorithms, code, deployment manifests, or operational commands.

## Requirement and analysis writing standard

Use stable IDs such as `SA-CTX-001`, `UC-ORD-001`, `FLOW-CHK-001`, `DATA-001`, `INT-001`, and `DEC-001`.

Each analysis statement should identify the source requirement, logical subject, responsibility, behavior or decision, status, and downstream design or verification impact. Use diagrams when they materially improve understanding, but describe the required meaning in text as well.

## Deliverable conventions

- Use Markdown headings, tables, and PlantUML diagrams as the primary views for logical relationships and flows; use text as the normative specification.
- Preserve section numbering when refining an existing analysis.
- Include source traceability, assumptions, risks, open decisions, review status, and version history.
- When no destination is specified, use `output/SA/SA-<project-name>.md`.
- Do not call the analysis approved or design-ready while material decisions, ownership, or source requirements remain unresolved.
