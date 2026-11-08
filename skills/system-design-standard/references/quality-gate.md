# System Design Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`. Do not hide a design gap behind an unapproved technology choice.

## Input readiness

- Mandatory task, system identity, and System Analysis baseline are present, or a provisional design is explicitly authorized.
- Applicable SRS/FRS, PRD/BRD, Change Request, UX/user-flow/wireframe/design-system, browser/device/locale/accessibility, security/privacy, performance, availability, recovery, observability, deployment, operational, integration, vendor, platform, migration, compatibility, and capacity inputs are supplied or explicitly marked `Not Applicable`.
- Optional benchmarks, prototypes, reference architectures, cost estimates, diagrams, and preferred technologies are not treated as blockers or approvals.

## Source and architecture

- Governing System Analysis and requirements are identified with version/status.
- The specialist routing matrix classifies architecture, interface/data, frontend design, quality attributes, delivery/operations, and independent review as `Required`, `Conditional`, or `Not Applicable`, with source-based rationale.
- Only routed concerns and document templates were loaded; accepted compact handoffs are written once to their authoritative targets, and material conflicts or unresolved decisions are reconciled or present in `open-decisions.md` before readiness.
- The Index links the applicable Backend, Frontend, Integration, and contract artifacts with versions/statuses and contains the routing/status table and review verdict.
- Backend, Frontend, and Integration documents respect their authority boundaries; full schemas and normative rules are not duplicated across documents.
- Machine-readable contract structure, Integration semantics, Backend internals, and Frontend internals agree; any authority conflict blocks readiness.
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
- API protocol semantics, field presence/nullability/defaults, duplicate and concurrent behavior, pagination, payload/rate limits, compatibility, deprecation, and contract verification are explicit where applicable.
- Error handling defines taxonomy/codes, throw-or-return and translation boundaries, public mappings, retryability, terminal handling, cause preservation, and single-owner logging where applicable.
- Data has a source of truth, owner, lifecycle, consistency boundary, access policy, retention/deletion rule, capacity assumption, and backup/recovery behavior.
- Persistent data defines datastore rationale, keys and constraints, bounded access paths, index evidence, transaction/isolation and conflict behavior, migration/backfill compatibility, connection capacity, and tested restore expectations where applicable.
- Every cache has a measurable purpose, source of truth, staleness/invalidation contract, key/value/TTL model, failure behavior, tenant/security controls, capacity, and observability; feature-specific cache use is not assumed.
- Messaging defines owner, contract/versioning, scoped delivery/ordering guarantees, publish consistency, consumer idempotency, acknowledgement/offset point, retries, DLQ/replay, security, capacity, and broker-version assumptions.
- Migrations, compatibility, and rollback implications are addressed when data or contracts change.
- When frontend scope exists, backend domain/data/transaction/security ownership is explicit; the versioned frontend/backend contract has joint journey-driven review and `Contract-Ready` status before parallel detail or implementation readiness.
- The frontend design covers applicable rendering/routing/modules, server/client and trust boundaries, components/design system, complete UI states, state/data ownership, responsive/accessibility/localization, performance, client security, observability, build/delivery, and test evidence without duplicating authoritative backend rules.
- Contract feedback resolves or registers request fan-out, client joins, field/error semantics, pagination/filter/sort, idempotency/concurrency, deadlines/cancellation, compatibility, mocks/examples, and unsupported UX needs.

## Critical behavior and resilience

- Critical flows have sequence/state/data-flow views or equivalent text.
- Success, failure, timeout, retry, duplicate, concurrency, fallback, compensation, and recovery behavior are covered where relevant.
- End-to-end deadlines and cancellation, single-owner bounded retries, circuit/isolation behavior, queue and concurrency limits, overload/load-shed policy, degraded modes, health semantics, reconciliation, failover, and failback are explicit where applicable.
- Cache loss/staleness/stampede and message duplication/delay/reordering/poison/failover behavior are covered when those technologies are used.
- Performance, availability, scalability, reliability, and disaster-recovery choices map to explicit targets or assumptions.
- Critical journeys define percentile latency/throughput objectives, representative workload/data assumptions, budgets, bottleneck evidence, capacity/headroom, scaling limits, dependency quotas, and regression verification where applicable.

## Security, privacy, and operations

- Identity, authentication, authorization, data isolation, secrets, encryption, audit, privacy, retention, and abuse controls are addressed.
- Assets, trust boundaries, data classifications, threats/abuse cases, enforcement points, owners, failure behavior, verification evidence, exceptions, and residual risks are explicit for every material security control.
- Authorization is server-side and covers use-case, object, tenant, field, state, privileged, batch/export, and workload access as applicable; interface or middleware checks are not treated as sufficient by themselves.
- Encryption decisions include purpose and data scope plus approved key ownership, storage, access, rotation, revocation, recovery, destruction, audit, and dependency-failure behavior; custom cryptography and silent plaintext fallback are absent.
- Logs, metrics, traces, alerts, dashboards, runbooks, ownership, deployment, rollback, configuration, backup, and restore are defined.
- Configuration defines key ownership/schema, source and precedence, validation, environment/tenant scope, refresh/stale behavior, secret boundaries, audit, drift, rollout, rollback, and provider-failure behavior where applicable.
- Deployment/release defines immutable artifact identity and promotion, mixed-version compatibility, migration order, rollout/exposure gates, health/drain behavior, rollback or roll-forward, approvals, and post-release evidence.
- Operability defines service/dependency ownership, SLIs/SLOs, actionable alerts, safe diagnostics, escalation, runbooks, incident handling, maintenance, drills, support expectations, and readiness evidence.
- Logging defines useful structured event/audit contracts, correlation, sensitive-data exclusions, retention/access, and noise/volume controls where applicable.
- Tracing defines meaningful operation boundaries, propagation, async/message causality, sampling, privacy, and cost without requiring a span for every function.
- Operational and support responsibilities are explicit and feasible.

## Decisions and traceability

- Technology choices and ADRs include alternatives, rationale, trade-offs, consequences, and approval status.
- Critical analysis requirements trace to design decisions, components/interfaces/data models, and verification evidence.
- Testing uses a risk-based portfolio with explicit levels/types, scenarios, environments, data, dependency strategy, non-functional evidence, flaky-test control, gates, results, and visible residual risk.
- Risks, dependencies, open decisions, and design limitations have owners or next actions when known.

## Boundary and readiness

- The applicable document set contains design, not production implementation or unauthorized external mutations.
- No secrets, credentials, or private production configuration are embedded.
- No persistent specialist packets, duplicate decision/conflict/routing registers, or separate review report exist unless a project/audit convention explicitly requires retention.
- `Contract-Ready`, Backend/Frontend/Integration readiness, and overall `SD-Ready` are recorded in the Index and are not called approved or implementation-ready while material requirements, decisions, controls, operational ownership, or sign-offs remain pending.
