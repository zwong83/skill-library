# System Analysis Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`. Do not convert a gap into an invented design choice.

## Input readiness

- Mandatory task, system identity, and requirements baseline are present.
- Applicable FRS, Change Request, security/privacy, performance, integration, data-retention, availability, recovery, and operational inputs are supplied or explicitly marked `Not Applicable`.
- Optional research, examples, diagrams, logs, and benchmarks are not treated as blockers or approvals.

## Source and scope

- Governing source documents are identified with version/status.
- System purpose, boundaries, scope, exclusions, actors, and release context are explicit.
- Assumptions, constraints, dependencies, and analysis limitations are distinguished from confirmed facts.

## Logical decomposition

- Capabilities map to source requirements and do not overlap ambiguously.
- Actors, roles, permissions, responsibilities, and operational handoffs are explicit.
- Important use cases include preconditions, triggers, main flow, alternate/exception paths, postconditions, and verification scenarios.
- State transitions, validation, idempotency, concurrency, expiry, recovery, audit, and observability are analyzed where relevant.

## Data and integration analysis

- Logical data concepts have ownership, lifecycle, consistency, history, retention, privacy, and access implications.
- Integrations have purpose, business data, timing, failure/fallback behavior, reconciliation, ownership, and approval status.
- Source-of-truth responsibilities and cross-boundary failure effects are clear.

## Quality and risk analysis

- Performance, capacity, availability, reliability, security, privacy, accessibility, compatibility, observability, recovery, and compliance impacts are considered where applicable.
- Risks, dependencies, alternatives, trade-offs, and open decisions have owners or next actions when known.

## Traceability and boundary

- Critical source requirements trace to capabilities/use cases, logical responsibilities, design inputs, and verification scenarios.
- The document does not silently include frameworks, physical schemas, endpoint contracts, class design, algorithms, deployment topology, or code.
- The handoff to System Design is explicit and complete enough to prevent design from guessing business behavior.

## Readiness

- Approval status and version history are present.
- Material unresolved scope, ownership, state, integration, security, or acceptance decisions are visible.
- The analysis is not called approved or design-ready while material decisions remain pending.
