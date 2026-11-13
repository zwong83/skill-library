# SRS Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`. Do not convert gaps into invented requirements.

## Input readiness

- Mandatory task, system identity, requirements baseline, and mode-specific source inputs are present.
- A new SRS can pass the input gate before the FRS is written. Detailed feature behavior belongs in the later FRS. If an existing approved or explicitly accepted FRS governs the scope, its relevant requirements are reflected in the SRS and traced to source IDs.
- Applicable security/privacy, performance, operational, integration, data-retention, and Change Request inputs are supplied or explicitly marked `Not Applicable`.
- Optional examples, diagrams, and implementation suggestions are not treated as blockers or approvals.

## Source and scope

- Source BRD/PRD or source waiver is identified with version/status.
- System purpose, actors, operating context, scope, exclusions, and release boundary are explicit.
- Assumptions, constraints, dependencies, and deferred capabilities are separated from confirmed requirements.

## Requirement quality

- Important requirements have stable IDs and one observable intent.
- Functional requirements identify actor/system responsibility, trigger, behavior, validation, exceptions, and acceptance criteria where relevant.
- Priorities and decision statuses are separate and used consistently.
- State transitions, idempotency, concurrency, history, access control, and failure behavior are specified when the domain requires them.

## Interfaces and data

- Relevant user, software, hardware, and communication interfaces are covered.
- Each external interface has a purpose, business data, timing, failure/fallback behavior, owner, and approval status.
- Logical data behavior, validation, lifecycle, retention, and access boundaries are clear.
- Physical schemas, endpoint contracts, and protocol details are not incorrectly presented as approved SRS requirements.

## Non-functional quality

- Applicable performance, availability, reliability, security, privacy, accessibility, compatibility, scalability, maintainability, observability, recovery, and compliance requirements are covered.
- Targets are measurable or clearly labeled `Proposed`/`TBC`.
- Sensitive data and security boundaries are explicit without embedding secrets or private configuration.

## Traceability and readiness

- Critical requirements trace to source objectives/goals and acceptance or UAT/test references.
- Acceptance criteria cover happy path, validation, permissions, empty state, failure, recovery, and boundary cases as relevant.
- Risks, dependencies, open decisions, approval status, and change control are visible.
- The document is not called approved or implementation-ready while material decisions or sign-offs remain pending.

## Boundary check

Flag endpoint contracts, database DDL, class design, frameworks, detailed algorithms, deployment topology, and unapproved technology choices for SA/SDS or an implementation plan.
