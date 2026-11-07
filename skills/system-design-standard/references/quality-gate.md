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
- Logical layers/modules have explicit responsibilities, allowed/forbidden dependencies, transaction/failure ownership, composition, and enforceable boundaries when applicable.
- When OOP or a hybrid paradigm is selected, high-level object responsibilities, identities/values, relationships, ownership, lifecycle, dependency direction, and stable contracts are explicit without duplicating detailed SDD class/method design.
- Object-oriented abstractions, SOLID guidance, and design patterns are not forced onto a language or problem where simpler native constructs are clearer.
- The design does not add components or complexity without a requirement or operational rationale.

## Diagram quality

- Architecture, component relationships, technical flows, states, data ownership, trust boundaries, and deployment are represented by focused diagrams when diagrams materially improve understanding.
- Each diagram has a title, scope, design explanation, source traceability, and required legend or assumptions.
- Diagrams are readable and answer one clear design question rather than combining unrelated views.
- Text remains authoritative for contracts, rules, constraints, exceptions, decisions, NFR targets, and operational procedures.
- Diagram and text do not conflict; any conflict is recorded and resolved before approval.

## Interfaces and data

- Interfaces define purpose, ownership, operations/messages, contracts, authentication/authorization, validation, errors, retries, timeouts, idempotency, versioning, and monitoring as applicable.
- Error handling defines taxonomy/codes, throw-or-return and translation boundaries, public mappings, retryability, terminal handling, cause preservation, and single-owner logging where applicable.
- Data has a source of truth, owner, lifecycle, consistency boundary, access policy, retention/deletion rule, capacity assumption, and backup/recovery behavior.
- Every cache has a measurable purpose, source of truth, staleness/invalidation contract, key/value/TTL model, failure behavior, tenant/security controls, capacity, and observability; feature-specific cache use is not assumed.
- Messaging defines owner, contract/versioning, scoped delivery/ordering guarantees, publish consistency, consumer idempotency, acknowledgement/offset point, retries, DLQ/replay, security, capacity, and broker-version assumptions.
- Migrations, compatibility, and rollback implications are addressed when data or contracts change.

## Critical behavior and resilience

- Critical flows have sequence/state/data-flow views or equivalent text.
- Success, failure, timeout, retry, duplicate, concurrency, fallback, compensation, and recovery behavior are covered where relevant.
- Cache loss/staleness/stampede and message duplication/delay/reordering/poison/failover behavior are covered when those technologies are used.
- Performance, availability, scalability, reliability, and disaster-recovery choices map to explicit targets or assumptions.

## Security, privacy, and operations

- Identity, authentication, authorization, data isolation, secrets, encryption, audit, privacy, retention, and abuse controls are addressed.
- Assets, trust boundaries, data classifications, threats/abuse cases, enforcement points, owners, failure behavior, verification evidence, exceptions, and residual risks are explicit for every material security control.
- Authorization is server-side and covers use-case, object, tenant, field, state, privileged, batch/export, and workload access as applicable; interface or middleware checks are not treated as sufficient by themselves.
- Encryption decisions include purpose and data scope plus approved key ownership, storage, access, rotation, revocation, recovery, destruction, audit, and dependency-failure behavior; custom cryptography and silent plaintext fallback are absent.
- Logs, metrics, traces, alerts, dashboards, runbooks, ownership, deployment, rollback, configuration, backup, and restore are defined.
- Logging defines useful structured event/audit contracts, correlation, sensitive-data exclusions, retention/access, and noise/volume controls where applicable.
- Tracing defines meaningful operation boundaries, propagation, async/message causality, sampling, privacy, and cost without requiring a span for every function.
- Operational and support responsibilities are explicit and feasible.

## Decisions and traceability

- Technology choices and ADRs include alternatives, rationale, trade-offs, consequences, and approval status.
- Critical analysis requirements trace to design decisions, components/interfaces/data models, and verification evidence.
- Risks, dependencies, open decisions, and design limitations have owners or next actions when known.

## Boundary and readiness

- The document contains design, not production implementation or unauthorized external mutations.
- No secrets, credentials, or private production configuration are embedded.
- The design is not called approved or implementation-ready while material requirements, decisions, controls, operational ownership, or sign-offs remain pending.
