# System Design Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`. Do not hide a design gap behind an unapproved technology choice.

## Input readiness

- Mandatory task, system identity, and System Analysis baseline are present, or a provisional design is explicitly authorized.
- Applicable SRS/FRS, PRD/BRD, Change Request, security/privacy, performance, availability, recovery, observability, deployment, operational, integration, vendor, platform, migration, compatibility, and capacity inputs are supplied or explicitly marked `Not Applicable`.
- Optional benchmarks, prototypes, reference architectures, cost estimates, diagrams, and preferred technologies are not treated as blockers or approvals.

## Source and architecture

- Governing System Analysis and requirements are identified with version/status.
- Architecture drivers, constraints, design principles, scope, and system boundaries are explicit.
- Major containers/components have clear responsibilities, ownership, dependencies, and trust boundaries.
- The design does not add components or complexity without a requirement or operational rationale.

## Interfaces and data

- Interfaces define purpose, ownership, operations/messages, contracts, authentication/authorization, validation, errors, retries, timeouts, idempotency, versioning, and monitoring as applicable.
- Data has a source of truth, owner, lifecycle, consistency boundary, access policy, retention/deletion rule, capacity assumption, and backup/recovery behavior.
- Migrations, compatibility, and rollback implications are addressed when data or contracts change.

## Critical behavior and resilience

- Critical flows have sequence/state/data-flow views or equivalent text.
- Success, failure, timeout, retry, duplicate, concurrency, fallback, compensation, and recovery behavior are covered where relevant.
- Performance, availability, scalability, reliability, and disaster-recovery choices map to explicit targets or assumptions.

## Security, privacy, and operations

- Identity, authentication, authorization, data isolation, secrets, encryption, audit, privacy, retention, and abuse controls are addressed.
- Logs, metrics, traces, alerts, dashboards, runbooks, ownership, deployment, rollback, configuration, backup, and restore are defined.
- Operational and support responsibilities are explicit and feasible.

## Decisions and traceability

- Technology choices and ADRs include alternatives, rationale, trade-offs, consequences, and approval status.
- Critical analysis requirements trace to design decisions, components/interfaces/data models, and verification evidence.
- Risks, dependencies, open decisions, and design limitations have owners or next actions when known.

## Boundary and readiness

- The document contains design, not production implementation or unauthorized external mutations.
- No secrets, credentials, or private production configuration are embedded.
- The design is not called approved or implementation-ready while material requirements, decisions, controls, operational ownership, or sign-offs remain pending.
