---
name: system-design-standard
description: Create or audit implementation-ready System Design documents covering architecture, component responsibilities, interfaces, data design, sequences, security, reliability, observability, deployment, trade-offs, and verification without writing production code.
---

# Standard System Design

Use this skill when the user wants to create, refine, compare, or quality-check a System Design document. The output turns an approved System Analysis and requirements baseline into an explicit, reviewable technical design that implementation and operations can follow.

This skill is self-contained. Do not invoke or inherit instructions from other skills unless the user explicitly asks for a separate artifact.

## Core operating rules

- Treat approved requirements, System Analysis, confirmed constraints, and explicit technical decisions as the source of truth.
- Read identified source material completely before designing.
- Never invent product scope, approval status, security policy, compliance obligation, capacity target, vendor approval, or operational ownership.
- Label uncertainty as `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Pending Approval`, `Open`, or `Deferred`.
- Make design decisions explicit: state the decision, context, alternatives, trade-offs, consequences, owner, and approval status.
- Prefer simple, explainable designs that satisfy the requirements. Do not add components, patterns, or infrastructure without a reason tied to a requirement or operational need.
- Treat security, privacy, reliability, observability, operability, cost, performance, and recovery as first-class design concerns.
- Do not generate production code, migration execution, deployment commands, or live infrastructure changes unless the user separately requests and authorizes them.

## Diagram dependency

When design needs a diagram, invoke/read `plantuml-syntax` before creating or modifying PlantUML and load only the relevant reference. Prefer C4 context/container/component, component, sequence, state, class, ER, deployment, and data-flow diagrams; every diagram must state its scope, assumptions, and design meaning in text.

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
4. Specify interfaces, contracts, error behavior, sequencing, timeouts, retries, idempotency, consistency, and versioning at the level needed for implementation review.
5. Define logical and physical data design as appropriate, including schema ownership, indexes/constraints, migrations, retention, privacy, and backup/recovery.
6. Design security, authorization, secrets handling, observability, availability, scalability, performance, disaster recovery, deployment, and operations.
7. Record alternatives, trade-offs, risks, dependencies, assumptions, and decisions.
8. Maintain traceability:

   `Analysis requirement/flow -> Design decision/component/interface/data model -> Verification evidence`

9. Run [references/quality-gate.md](references/quality-gate.md) before delivery.
10. End with implementation prerequisites, open decisions, approval status, and the next design-review action.

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

- Use Markdown headings, tables, Mermaid or PlantUML diagrams, and code blocks for schemas/contracts only when they clarify the design.
- Preserve section numbering when refining an existing design.
- Include source traceability, decision records, risks, dependencies, approval status, version history, and change control.
- When no destination is specified, use `output/SD/SD-<project-name>.md`.
- Do not call the design approved or implementation-ready while material requirements, design decisions, interfaces, security controls, operational ownership, or sign-offs remain pending.
