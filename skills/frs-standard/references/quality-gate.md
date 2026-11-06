# FRS Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`. Do not turn a gap into an invented behavior.

## Input readiness

- Mandatory task, feature identity, source requirement, and mode-specific inputs are present.
- Applicable SRS, PRD/BRD, security/privacy, accessibility, performance, operational, integration, UX, and Change Request inputs are supplied or explicitly marked `Not Applicable`.
- Optional examples, screenshots, diagrams, and supplementary references are not treated as blockers or approvals.

## Source, scope, and actors

- Source SRS/PRD/BRD or source limitation is identified with version/status.
- Feature purpose, user outcome, in-scope behavior, exclusions, release, actors, roles, and permissions are explicit.
- Preconditions, triggers, postconditions, and dependencies are visible.

## Functional behavior

- Each important behavior has a stable ID and one observable intent.
- Main, alternate, validation, permission, empty, failure, retry, and recovery paths are covered as relevant.
- Inputs, calculations, validation boundaries, state transitions, side effects, notifications, and retention behavior are specified where applicable.
- Requirements use consistent priority and decision-status schemes.
- Concurrency, idempotency, expiry, duplicate submission, and reconciliation behavior are covered when the domain requires them.

## Acceptance and traceability

- Critical behavior has binary, testable acceptance criteria.
- Acceptance criteria cover happy path, validation, permissions, boundary conditions, failures, and recovery as relevant.
- Functional requirements trace to source requirements and UAT/test references.
- Cross-feature dependencies and rule precedence are explicit.

## Quality and boundary

- Feature-specific security, privacy, accessibility, compatibility, performance, and reliability implications are linked to SRS requirements or clearly labeled.
- External behavior is described at the business/functional level.
- Endpoint contracts, database DDL, class design, frameworks, algorithms, deployment topology, and unapproved technology choices are not incorrectly embedded in the FRS.

## Decision and delivery readiness

- Assumptions, TBC items, pending approvals, open questions, and risks are distinguishable.
- The document includes approval status, version history, and change-control rules where material.
- The FRS is not called approved, complete, or implementation-ready while material behavior, permissions, dependencies, acceptance criteria, or sign-offs remain pending.
