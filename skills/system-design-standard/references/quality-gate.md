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
- Machine-readable contract structure, database physical artifacts, Integration semantics, Backend data/runtime semantics, and Frontend internals agree; any authority conflict blocks readiness.
- Architecture drivers, constraints, design principles, scope, and system boundaries are explicit.
- Major containers/components have clear responsibilities, ownership, dependencies, and trust boundaries.
- Logical layers/modules have explicit responsibilities, allowed/forbidden dependencies, transaction/failure ownership, composition, and enforceable boundaries when applicable.
- When OOP or a hybrid paradigm is selected, high-level object responsibilities, identities/values, relationships, ownership, lifecycle, dependency direction, and stable contracts are explicit without duplicating detailed SDD class/method design.
- Object-oriented abstractions, SOLID guidance, and design patterns are not forced onto a language or problem where simpler native constructs are clearer.
- The design does not add components or complexity without a requirement or operational rationale.

## Diagram quality

- The feature/diagram coverage matrix contains every in-scope feature, source/SA IDs, owner, target document, diagram IDs, conditional views, verification, and status.
- A full design contains target architecture and main runtime-flow views plus current architecture/main-flow/problem views for brownfield scope.
- Every feature has a dedicated target technical-flow sequence/activity diagram; each changed brownfield feature also has an evidence-based current path and problem IDs.
- Stateful, data-changing, cross-boundary, middleware-using, and user-facing features have the applicable state, data/transaction, integration/middleware, and frontend route/component/state views or a source-based `Not Applicable` rationale.
- Applicable physical ERD, deployment/middleware topology, trust-boundary/control, and failure/recovery diagrams are present.
- Each diagram has a title, scope, design explanation, source traceability, and required legend or assumptions.
- Each diagram has a stable ID, As-Is/To-Be status, feature/decision traceability, and owner.
- Diagrams are readable and answer one clear design question rather than combining unrelated views.
- Text is concise and adds only exact contracts, rules, parameters, constraints, exceptions, decisions, NFR targets, procedures, traceability, and unresolved items instead of repeating visual content.
- Diagram and text do not conflict; any conflict is recorded and resolved before approval.
- Diagram IDs resolve to maintained PlantUML sources; authoritative sections link them, rendered previews are embedded when tooling is available, and claimed syntax/render validation has actual evidence.

## Interfaces and data

- Interfaces define purpose, ownership, operations/messages, contracts, authentication/authorization, validation, errors, retries, timeouts, idempotency, versioning, and monitoring as applicable.
- API protocol semantics, field presence/nullability/defaults, duplicate and concurrent behavior, pagination, payload/rate limits, compatibility, deprecation, and contract verification are explicit where applicable.
- Error handling defines taxonomy/codes, throw-or-return and translation boundaries, public mappings, retryability, terminal handling, cause preservation, and single-owner logging where applicable.
- Data has a source of truth, owner, lifecycle, consistency boundary, access policy, retention/deletion rule, capacity assumption, and backup/recovery behavior.
- Persistent data defines datastore rationale, keys and constraints, bounded access paths, index evidence, transaction/isolation and conflict behavior, migration/backfill compatibility, connection capacity, and tested restore expectations where applicable.
- Every data-changing scope has conceptual/logical/physical models, an owned data dictionary, dialect/version-specific proposed DDL for affected structures, and traceability from feature/data IDs to schema artifacts.
- Every state-changing operation and critical read path appears in a parameterized DML/query catalog with bounds, transaction, lock/conflict, index/access path, result/error, and verification.
- Transaction/concurrency, indexes/access paths, migration/backfill/validation, compatibility, rollback or recovery, retention/deletion, backup/restore, pooling, capacity, and observability artifacts are complete where applicable.
- Every cache has a measurable purpose, source of truth, staleness/invalidation contract, key/value/TTL model, failure behavior, tenant/security controls, capacity, and observability; feature-specific cache use is not assumed.
- Messaging defines owner, contract/versioning, scoped delivery/ordering guarantees, publish consistency, consumer idempotency, acknowledgement/offset point, retries, DLQ/replay, security, capacity, and broker-version assumptions.
- The middleware register lists every current/proposed database, cache, queue/stream, search, scheduler, object-storage, or equivalent dependency with feature mapping, purpose, product/version or unresolved decision, owner, topology, contract/data, consistency, failure/recovery, capacity, security, observability, operations, and status.
- Every selected middleware has a topology/deployment view and per-feature interaction sequence; middleware is not introduced without a requirement and explicit rationale.
- Migrations, compatibility, and rollback implications are addressed when data or contracts change.
- When frontend scope exists, backend domain/data/transaction/security ownership is explicit; the versioned frontend/backend contract has joint journey-driven review and `Contract-Ready` status before parallel detail or implementation readiness.
- The frontend design covers applicable rendering/routing/modules, server/client and trust boundaries, components/design system, complete UI states, state/data ownership, responsive/accessibility/localization, performance, client security, observability, build/delivery, and test evidence without duplicating authoritative backend rules.
- Contract feedback resolves or registers request fan-out, client joins, field/error semantics, pagination/filter/sort, idempotency/concurrency, deadlines/cancellation, compatibility, mocks/examples, and unsupported UX needs.

## Critical behavior and resilience

- Every feature has visual technical logic; critical cross-feature journeys additionally have end-to-end sequence/state/data-flow views.
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

- Technology choices and ADRs include driver, selected decision, rationale, consequences, owner, and approval status; solution-comparison tables are not required.
- Critical analysis requirements trace to design decisions, components/interfaces/data models, and verification evidence.
- Testing uses a risk-based portfolio with explicit levels/types, scenarios, environments, data, dependency strategy, non-functional evidence, flaky-test control, gates, results, and visible residual risk.
- Risks, dependencies, open decisions, and design limitations have owners or next actions when known.

## Boundary and readiness

- The applicable document set contains design, not production implementation or unauthorized external mutations.
- No secrets, credentials, or private production configuration are embedded.
- No persistent specialist packets, duplicate decision/conflict/routing registers, or separate review report exist unless a project/audit convention explicitly requires retention.
- `Contract-Ready`, Backend/Frontend/Integration readiness, and overall `SD-Ready` are recorded in the Index and are not called approved or implementation-ready while material requirements, decisions, controls, operational ownership, or sign-offs remain pending.
- Applicable `Data-Ready` and `Middleware-Ready` statuses are recorded, and no readiness claim is made while feature diagram, DDL/DML, data model, transaction, migration, or middleware coverage is incomplete.
