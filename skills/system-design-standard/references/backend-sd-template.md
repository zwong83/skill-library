# Backend System Design Template

Use this document for backend internals and server-side enforcement. Reference Integration SD and machine-readable contracts for cross-boundary semantics and schema structure instead of duplicating them.

## Document control and scope

Record version/status, owner, target release, source IDs, in-scope backend capabilities, out-of-scope items, constraints, assumptions, and linked Index/Integration/contract versions.

## 1. Architecture drivers and context

Define functional and quality drivers, design principles, system boundary, neighboring systems, trust boundaries, major backend containers/components, and request/data flow. Use focused context/container diagrams when useful.

## 2. Components, modules, and dependencies

Define responsibilities, ownership, lifecycle, allowed/forbidden dependencies, composition root, ports/adapters where selected, transaction/failure ownership, and test seams. Do not force a layer count or OOP model.

Use `backend-layered-architecture-standard` when boundaries or dependency direction are material. Use `object-oriented-design`, `solid-principles`, or `design-patterns` only when the selected implementation paradigm and real design decision require them.

## 3. Domain, data, and persistence

Define authoritative domain rules, source of truth, logical/physical data model, keys/constraints, access paths, transactions/isolation/conflict behavior, lifecycle, privacy, retention/deletion, migration/backfill compatibility, indexing/partitioning/capacity assumptions, backup/restore, and recovery.

Use `backend-database-persistence-standard` when durable state changes. Diagrams may show entities, relationships, cardinality, ownership, and data flow; text owns invariants and consistency rules.

## 4. Internal behavior and flows

Define critical backend sequences, state machines, concurrency/ordering, timeout/cancellation, retry ownership, compensation, reconciliation, and failure/recovery behavior. Reference Integration SD for behavior crossing the backend boundary.

## 5. Cache and messaging

When applicable, define cache purpose/source of truth/key-value/TTL/invalidation/staleness/fallback/security/capacity/observability and message ownership/contract reference/topology/delivery/ordering/publish coordination/idempotency/acknowledgement/retry/dead-letter/replay/security/capacity/operations.

Use `backend-caching-standard` and `backend-messaging-standard` only when those technologies are selected. Load only the selected broker reference.

## 6. Server security and privacy

Define identity validation, server authorization and isolation, trust boundaries, data classification/protection, secrets/key boundaries, audit, abuse controls, privacy/retention/deletion, dependency/runtime security, control ownership, safe failure, verification, exceptions, and residual risks. Never delegate authoritative authorization to the client.

## 7. Error handling and resilience

Define internal error taxonomy, throw/result/catch/translation boundaries, cause preservation, terminal handling, retryability, single-owner logging, end-to-end deadlines, bounded retries, circuits, bulkheads, overload/load shedding, degradation, health, failover/failback, and integrity reconciliation.

Reference Integration SD for public error semantics.

## 8. Performance and capacity

Define measurable latency/throughput targets or labeled assumptions, workload/data model, budgets, bottlenecks, quotas, concurrency, headroom, scaling limits, dependency capacity, failover capacity, and required evidence.

## 9. Configuration, observability, and operations

Define configuration schema/source/precedence/validation/scope/refresh/drift/secret boundaries; logs/metrics/traces/audit and correlation; SLIs/SLOs, dashboards, alerts, diagnostics, ownership, runbooks, incidents, maintenance, support, and exercises. Keep statement-level instrumentation in SDD.

## 10. Deployment, release, and recovery

Define immutable artifact identity/provenance, environments/promotion, topology, compatibility, migration/configuration order, rollout/exposure, health/drain, rollback/roll-forward, backup/restore, disaster recovery, approvals, and post-release evidence. Reference Integration SD for mixed-version cross-boundary behavior.

## 11. Technology decisions and ADRs

Retain only material decisions with driver, selected option, meaningful alternatives, rationale, trade-offs, consequences, owner, and status. Record deferred material decisions explicitly.

## 12. Verification and handoff

Map requirement/SA IDs to backend decisions and unit/component, integration, contract, security, performance, resilience, migration, compatibility, and operational evidence. Record backend implementation prerequisites, sequencing, risks, dependencies, residual limitations, and Backend-Ready recommendation.
