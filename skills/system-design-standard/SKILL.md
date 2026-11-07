---
name: system-design-standard
description: Create or audit implementation-ready System Design documents covering architecture, component responsibilities, interfaces, data design, sequences, security, reliability, observability, deployment, trade-offs, and verification without writing production code.
---

# Standard System Design

Use this skill when the user wants to create, refine, compare, or quality-check a System Design document. The output turns an approved System Analysis and requirements baseline into an explicit, reviewable technical design that implementation and operations can follow.

This skill is the governing System Design standard. Invoke conditional companion skills only where this standard directs and only when they fit the selected paradigm or design problem.

## Core operating rules

- Treat approved requirements, System Analysis, confirmed constraints, and explicit technical decisions as the source of truth.
- Read identified source material completely before designing.
- Never invent product scope, approval status, security policy, compliance obligation, capacity target, vendor approval, or operational ownership.
- Label uncertainty as `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Pending Approval`, `Open`, or `Deferred`.
- Make design decisions explicit: state the decision, context, alternatives, trade-offs, consequences, owner, and approval status.
- Prefer simple, explainable designs that satisfy the requirements. Do not add components, patterns, or infrastructure without a reason tied to a requirement or operational need.
- When the system uses an object-oriented or hybrid implementation model, invoke/read `object-oriented-design` for high-level responsibilities, identity/value semantics, relationships, ownership, contracts, dependency direction, and class/object modeling. Do not force OOP onto a functional, data-oriented, Go, Rust, or other language-native design.
- When a reusable design pattern is relevant, invoke/read `design-patterns` as a conditional reference. Use its language-neutral guidance first and load language-specific mapping only when the target language is known; never force a pattern into the design.
- Treat security, privacy, reliability, observability, operability, cost, performance, and recovery as first-class design concerns.
- Do not generate production code, migration execution, deployment commands, or live infrastructure changes unless the user separately requests and authorizes them.

## Diagram-first policy

Use diagrams as the primary representation when the design explains architecture, relationships, boundaries, flows, hierarchy, state, timing, deployment, or data ownership. Prefer C4 context/container/component, component, sequence, state, class, ER, deployment, and data-flow diagrams.

- Invoke/read `plantuml-syntax` before creating or modifying PlantUML and load only the relevant reference.
- Invoke/read `object-oriented-design` before producing a class/object model or making a material inheritance, composition, interface, or object-lifecycle decision.
- Invoke/read `design-patterns` only when the design contains a pattern choice, pattern comparison, or reusable collaboration whose trade-offs need to be documented.
- Use one focused diagram per design question; do not combine unrelated architecture views into an unreadable diagram.
- Keep text as the authoritative source for contracts, rules, constraints, assumptions, exceptions, decisions, NFR targets, and operational procedures.
- Every diagram must state its title, scope, assumptions, design meaning, source traceability, and required legend.
- If a diagram and text conflict, the explicit text or ADR governs and the conflict must be fixed before approval.
- Do not add a diagram when a table or short design explanation is clearer.

## Input classification

### Mandatory inputs

- Task mode: draft, refine, compare, or review.
- System/product/feature identity and target release/scope when known.
- A complete System Analysis for new design work, unless the user explicitly authorizes a provisional design.
- The complete existing System Design for refinement or review.

### Conditional inputs

- SRS and FRS are mandatory when their requirements affect the design; otherwise record the limitation.
- PRD/BRD is mandatory when product scope, business rules, or acceptance constraints affect a design decision.
- A Change Request is mandatory for change-focused design, but not for greenfield design.
- Security/privacy, performance, availability, recovery, observability, deployment, operational, integration, vendor, and platform constraints are mandatory when applicable; if not applicable, record `Not Applicable`.
- Existing architecture, migration constraints, compatibility requirements, and capacity baselines are mandatory when the design decision depends on them.

### Optional context

- Benchmarks, prototypes, reference architectures, cost estimates, diagrams, and preferred technologies are optional unless a decision depends on them.

## Source and readiness gate

1. Classify the task as drafting, refining, comparing, or reviewing System Design.
2. Identify the governing System Analysis, requirements, approved constraints, and technical standards. Record versions/statuses.
3. Read the source material completely and verify that scope, behavior, actors, states, data ownership, integrations, and quality expectations are sufficiently defined.
4. If System Analysis is missing or material source decisions are unresolved, ask for the source or clearly mark the design as provisional. Do not conceal the gap with implementation assumptions.
5. Block an implementation-ready conclusion when material architecture, interface, data, security, performance, reliability, deployment, or operational decisions remain unresolved.

## Workflow

1. Read [references/system-design-template.md](references/system-design-template.md) for a full draft or structural review.
2. Establish architecture drivers, constraints, quality attributes, design principles, and decision criteria.
3. Define system context, containers/modules/components, responsibilities, trust boundaries, data flows, and ownership.
4. When OOP is selected, define only the high-level domain/object responsibilities, identities, values, relationships, dependency direction, and contracts needed for architecture review; defer detailed class/method design to SDD.
5. Specify interfaces, contracts, error behavior, sequencing, timeouts, retries, idempotency, consistency, and versioning at the level needed for implementation review.
6. Define logical and physical data design as appropriate, including schema ownership, indexes/constraints, migrations, retention, privacy, and backup/recovery.
7. Design security, authorization, secrets handling, observability, availability, scalability, performance, disaster recovery, deployment, and operations.
8. Record alternatives, trade-offs, risks, dependencies, assumptions, and decisions.
9. Maintain traceability:

   `Analysis requirement/flow -> Design decision/component/interface/data model -> Verification evidence`

10. Run [references/quality-gate.md](references/quality-gate.md) before delivery.
11. End with implementation prerequisites, open decisions, approval status, and the next design-review action.

## Design artifact boundaries

System Design may include:

- architecture context, container/component boundaries, responsibilities, and rationale;
- logical and physical data models when required by the design;
- API/interface contracts, protocols, authentication, versioning, and error models;
- sequence, state, data-flow, and deployment views;
- security, privacy, resilience, performance, scalability, observability, backup, recovery, and operations design;
- technology choices, alternatives, trade-offs, risks, and decision records when approved or clearly proposed.

Keep these out unless separately requested:

- production code or generated implementation files;
- live deployment, infrastructure mutation, database migration execution, or external system changes;
- unapproved secrets, credentials, private configuration, or vendor commitments.

## Design writing standard

Use stable IDs such as `DES-ARCH-001`, `CMP-001`, `API-001`, `DATA-001`, `SEQ-001`, `SEC-001`, `NFR-001`, `ADR-001`, and `TEST-001`.

For each design decision, state the requirement or analysis driver, selected approach, alternatives, rationale, consequences, assumptions, risks, and approval status. A diagram must have a textual explanation of its boundaries and behavior.

## Deliverable conventions

- Use Markdown headings, tables, PlantUML diagrams, and code blocks for schemas/contracts; diagrams should be the primary views for architecture and technical flows, while text remains normative.
- Preserve section numbering when refining an existing design.
- Include source traceability, decision records, risks, dependencies, approval status, version history, and change control.
- When no destination is specified, use `output/SD/SD-<project-name>.md`.
- Do not call the design approved or implementation-ready while material requirements, design decisions, interfaces, security controls, operational ownership, or sign-offs remain pending.
