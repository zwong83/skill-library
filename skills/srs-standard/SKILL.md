---
name: srs-standard
description: Create or audit implementation-ready Software Requirements Specifications with system context, functional and non-functional requirements, external interfaces, data behavior, traceability, acceptance, and approval control; use for software requirements, not architecture or code design.
---

# Standard Software Requirements Specification

Use this skill when the user wants to create, refine, compare, or quality-check an SRS. The SRS translates approved business and product intent into complete software-level requirements that development, QA, operations, and stakeholders can use as a shared reference.

## Core operating rules

- Treat the supplied BRD, PRD, applicable approved or explicitly accepted FRS, stakeholder decisions, and confirmed constraints as governing sources.
- Read identified source documents completely before transforming them into an SRS.
- Never invent scope, users, targets, dates, budgets, approvals, interfaces, security policies, technology choices, or legal conclusions.
- Label uncertainty explicitly as `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Pending Approval`, or `Deferred`.
- Separate requirements from design decisions. The SRS states what the system must do and the quality it must provide; architecture and implementation artifacts state how.
- Use atomic, observable, testable requirements. Avoid vague terms such as “fast”, “secure”, “user-friendly”, or “real-time” without measurable criteria.
- Do not silently resolve source conflicts. Record them as open decisions and identify the required owner.
- Do not generate API contracts, database DDL, class designs, framework instructions, deployment topology, or code unless the user separately requests that artifact.

## Diagram dependency

When an SRS needs a diagram, invoke/read `plantuml-syntax` before creating or modifying PlantUML and load the relevant reference only. Use diagrams for system context, use cases, workflows, states, logical data, or interfaces when they improve reviewability; keep the requirement and acceptance meaning in text.

## Input classification

### Mandatory inputs

- Task mode: draft, refine, compare, or review.
- System, product, project, or feature identity and target release/scope when known.
- A governing requirements baseline for new work, such as an approved/accepted BRD, PRD, or equivalent requirements statement.
- The complete existing SRS for refinement or review.

### Conditional inputs

- When an approved or explicitly accepted FRS already governs an in-scope feature, read it and trace the affected SRS requirements to its relevant IDs. A new SRS can be written before the FRS. Use the governing requirements baseline for system requirements and leave detailed feature flows, states, and validation scenarios for the later FRS.
- Security/privacy, performance, compatibility, availability, recovery, operational, integration, and data-retention constraints are mandatory when applicable; if not applicable, record `Not Applicable`, not silence.
- A Change Request is mandatory for change-focused SRS work, but not for greenfield work.
- Wireframes, interface examples, research, and test evidence are mandatory only when the requested SRS decision depends on them.

### Optional context

- Examples, diagrams, preferred notation, supplementary references, and implementation suggestions are optional and must be labeled if used.

## Source and readiness gate

1. Classify the request as drafting, refining, comparing, or reviewing an SRS.
2. Identify the governing BRD, PRD, approved change request, applicable existing approved or explicitly accepted FRS, or other source. Record title, version/date, status, and location when available. If no FRS exists yet, proceed from the governing baseline. If an applicable approved FRS exists but is unavailable, record the missing source and surface it before claiming readiness for affected requirements.
3. If a source is supplied, read it fully and preserve its decision status and terminology.
4. If no source is supplied, ask for the source or clearly state that the SRS will be source-light and cannot claim business approval.
5. If a source contains unresolved decisions that affect system behavior, scope, acceptance, security, data, or interfaces, surface them before calling the SRS implementation-ready. Do not turn them into confirmed requirements.

## Workflow

1. Read [references/srs-template.md](references/srs-template.md) for a full draft or structural review.
2. Extract system purpose, scope, actors, environments, constraints, dependencies, and approved product behavior.
3. Convert product behavior into stable requirement IDs. Use separate namespaces for system behavior, functional behavior, non-functional quality, external interfaces, data, security, and operations where useful.
4. For every critical requirement, capture actor, trigger/precondition, expected behavior, validation and failure behavior, priority, decision status, acceptance criteria, dependency, and release.
5. Specify external interfaces at the requirement level: purpose, exchanged business data, timing, availability expectation, failure/fallback behavior, ownership, and approval status. Keep endpoint and protocol details in a technical design artifact.
6. Specify NFRs with measurable targets or mark them `Proposed`/`TBC`. Cover applicable performance, availability, reliability, security, privacy, accessibility, compatibility, scalability, maintainability, observability, backup/recovery, and compliance needs.
7. Maintain traceability:

   `BRD objective / PRD goal -> SRS requirement -> Acceptance criterion -> UAT or test reference`

8. Run [references/quality-gate.md](references/quality-gate.md) before delivery.
9. End with unresolved decisions, assumptions, dependencies, approval status, and the next review action.

## Requirement writing standard

Prefer statements such as:

> `SYS-ORD-001` — The system shall create one unique order record for each accepted checkout request.
>
> `NFR-PERF-001` — Under the agreed load profile, the system shall return catalog search results within the approved p95 target.

Each important requirement should make clear:

- actor or system responsibility;
- trigger or entry condition;
- observable behavior or quality constraint;
- validation, exception, and recovery behavior where relevant;
- priority, decision status, and release;
- acceptance criteria;
- dependency and traceability references.

## SRS boundary

The SRS may include logical data behavior, business rules, external interface expectations, and quality attributes. It must not silently become an architecture or implementation document. Move the following to SA/SDS/SRS-Technical or an implementation plan:

- endpoint paths, payload schemas, protocol details, and authentication flows;
- physical database tables, indexes, DDL, and migration scripts;
- frameworks, packages, class/module layouts, algorithms, and deployment topology;
- unapproved vendor or technology decisions.

## Deliverable conventions

- Use Markdown headings and tables for scanning and comparison.
- Keep section numbering stable when refining an existing SRS.
- Include document control, source traceability, approval status, version history, and change-control rules for material work.
- When no destination is supplied, use `output/SRS/SRS-<project-name>.md`.
- Do not call the SRS approved, implementation-ready, or complete while material decisions, interfaces, NFR targets, or sign-offs remain pending.
