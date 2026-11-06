---
name: frs-standard
description: Create or audit detailed Functional Requirements Specifications with feature behavior, workflows, states, validation, permissions, exceptions, acceptance criteria, traceability, and change control; use for functional behavior, not architecture or code design.
---

# Standard Functional Requirements Specification

Use this skill when the user wants to create, refine, compare, or quality-check an FRS for a product or feature. The FRS translates approved business/product/system intent into detailed, testable functional behavior that developers and QA can implement and verify without guessing.

## Core operating rules

- Treat the supplied SRS, PRD, BRD, approved change request, and confirmed stakeholder decisions as the source of truth.
- Read identified source documents completely before writing or auditing the FRS.
- Never invent actors, scope, policies, data, permissions, metrics, dates, integrations, technology choices, or approvals.
- Label uncertainty explicitly as `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Pending Approval`, or `Deferred`.
- Describe what the product/system must do, not how it will be coded or deployed.
- Use atomic, observable, testable requirements. Each requirement should have a clear actor/system responsibility and expected outcome.
- Do not silently resolve contradictions. Record them as open decisions with the decision owner when known.
- Keep a feature's behavior, states, validation, permissions, failures, and acceptance criteria together so the FRS can serve as a build and QA reference.

## Diagram dependency

When an FRS needs a diagram, invoke/read `plantuml-syntax` before creating or modifying PlantUML and load the relevant reference only. Prefer use-case, activity, sequence, state, or wireframe diagrams for feature behavior; keep all required functional behavior and acceptance criteria in text.

## Input classification

### Mandatory inputs

- Task mode: draft, refine, compare, or review.
- Feature/system identity, user or business goal, and target release/scope when known.
- At least one authoritative source requirement or an explicit user-provided functional brief for new work.
- The complete existing FRS for refinement or review.

### Conditional inputs

- SRS is mandatory when system constraints, interfaces, data behavior, or cross-feature dependencies affect the requested FRS; otherwise record the limitation explicitly.
- PRD/BRD is mandatory when product goals, business rules, scope, or approval constraints affect the feature.
- Security/privacy, accessibility, performance, operational, integration, UX, and Change Request inputs are mandatory when applicable; if not applicable, record `Not Applicable`.
- Wireframes, API examples, test data, and UAT evidence are mandatory only when the requested behavior or acceptance depends on them.

### Optional context

- Screenshots, examples, preferred wording, supplementary diagrams, and competitor references are optional and do not constitute approval.

## Source and readiness gate

1. Classify the request as drafting, refining, comparing, or reviewing an FRS.
2. Identify the governing SRS, PRD, BRD, approved change request, or feature decision. Record source version/status when available.
3. Prefer an approved or explicitly accepted SRS for system constraints. If no SRS exists, ask whether the user wants to proceed from the PRD/BRD and clearly mark technical/system details as `TBC`.
4. If source material contains unresolved decisions that affect feature behavior, permission, data, acceptance, or release, surface them before calling the FRS complete.
5. Do not silently use architecture or implementation assumptions to close a functional gap.

## Workflow

1. Read [references/frs-template.md](references/frs-template.md) for a full draft or structural review.
2. Define the feature boundary, actors, user goal, related source requirements, preconditions, trigger, main flow, alternate flows, failure/recovery flows, postconditions, and release.
3. Assign stable IDs. Use `FR-<AREA>-nnn` for functional requirements, `UC-<AREA>-nnn` for use cases/workflows, and `AC-<AREA>-nnn` for acceptance criteria when useful.
4. For every major feature, specify:
   - entry points and preconditions;
   - main and alternate user/system flows;
   - states and allowed transitions;
   - input, calculation, validation, and boundary rules;
   - permissions and role behavior;
   - loading, empty, success, error, retry, and recovery states;
   - notifications and observable side effects;
   - business-level data created, read, changed, or retained;
   - dependencies and external behavior;
   - acceptance criteria and traceability.
5. Use Given/When/Then or concise expected-result tables for critical paths.
6. Keep NFR references linked from the SRS or record feature-specific quality constraints without duplicating the entire SRS.
7. Maintain traceability:

   `BRD objective / PRD goal -> SRS requirement -> FRS feature/use case -> Functional requirement -> Acceptance criterion -> UAT/test`

8. Run [references/quality-gate.md](references/quality-gate.md) before delivery.
9. End with open decisions, assumptions, dependencies, approval status, and the next review action.

## Functional requirement writing standard

Prefer statements such as:

> `FR-CHK-001` — When the customer submits a valid checkout, the system shall validate availability, calculate the approved total, create one order, and display the order reference.

Each requirement should make clear:

- actor or system responsibility;
- trigger, precondition, and relevant context;
- exact behavior and observable result;
- validation, permission, exception, and recovery behavior;
- priority, decision status, release, and dependencies;
- acceptance criteria and traceability.

## FRS boundary

The FRS may describe user-visible behavior, business-level data, state transitions, validations, permissions, notification triggers, and external behavior. Move the following to SA/SDS/technical design:

- endpoint paths, payload schemas, protocol details, service classes, database DDL, frameworks, algorithms, deployment topology, and infrastructure configuration;
- unapproved implementation choices presented as if they were functional requirements;
- detailed visual styling that is not required for behavior or accessibility.

## Deliverable conventions

- Use Markdown headings and tables for scanning and test-case preparation.
- Keep section numbering stable when refining an existing FRS.
- Include source traceability, approval status, version history, and change control for material work.
- When no destination is supplied, use `output/FRS/FRS-<project-name>.md`.
- Do not call the FRS approved, complete, or ready for implementation while material behavior, permissions, dependencies, acceptance criteria, or sign-offs remain pending.
