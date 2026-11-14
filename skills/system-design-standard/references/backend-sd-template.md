# Backend System Design Template

Use this document for backend internals and server-side enforcement. Reference Integration SD and machine-readable contracts for cross-boundary semantics and schema structure instead of duplicating them.

## Document control and scope

Record version/status, owner, target release, source IDs, in-scope backend capabilities, out-of-scope items, constraints, assumptions, linked Index/Integration/contract/database-artifact versions, and the feature/diagram coverage matrix location.

## 1. Architecture drivers and context

Define functional and quality drivers, design principles, system boundary, neighboring systems, trust boundaries, major backend containers/components, and request/data flow.

For brownfield scope, include current context/container/deployment views and the current main runtime flow with problem IDs. Always include target context/container/component architecture and the target main runtime flow. Keep current and target facts visually distinct.

## 2. Components, modules, and dependencies

Define responsibilities, ownership, lifecycle, allowed/forbidden dependencies, composition root, ports/adapters where selected, transaction/failure ownership, and test seams. Include a component/dependency diagram that maps feature IDs to owning modules. Do not force a layer count or OOP model.

Use `backend-layered-architecture-standard` when boundaries or dependency direction are material. Use the relevant `clean-code-standard` references for object modeling, SOLID, or patterns when a material design decision requires them.

## 3. Feature technical design

Create one visual-first feature block for every backend feature using [feature-diagram-coverage.md](feature-diagram-coverage.md). Each block must include a dedicated target sequence/activity diagram with components, calls/events, decisions, transaction boundaries, durable effects, middleware interactions, and observable result. Show applicable validation, authorization, timeout, retry, duplicate, concurrency, partial failure, compensation, fallback, and terminal paths. Brownfield changes also include or link their current runtime path and problem IDs.

Follow the reference's fixed per-feature construction: focused technical sequence(s), engineering-constraint table, interface/data/middleware impact table, and error/result table. Use short tables for exact rules, parameters, interfaces, errors, NFR targets, decisions, and verification. Do not repeat diagram narration in prose.

## 4. Domain, data, DDL, DML, and persistence

Define authoritative domain rules, source of truth, conceptual/logical/physical data models, keys/constraints, access paths, transactions/isolation/conflict behavior, lifecycle, privacy, retention/deletion, migration/backfill compatibility, indexing/partitioning/capacity assumptions, backup/restore, and recovery.

Use `db-standard` and [data-and-middleware-artifacts.md](data-and-middleware-artifacts.md) when durable state changes. Require a physical ERD, data dictionary, dialect/version-specific proposed DDL for affected structures, feature-linked parameterized DML/query catalog, transaction/concurrency matrix, index/access-path plan, and migration/backfill/validation/recovery artifacts. Link authoritative files under `output/SD/database/`; do not paste full copies into this document.

## 5. Internal behavior and flows

Define cross-feature backend sequences, state machines, concurrency/ordering, timeout/cancellation, retry ownership, compensation, reconciliation, and failure/recovery behavior. Per-feature behavior belongs in Section 3. Reference Integration SD for behavior crossing the backend boundary.

## 6. Middleware: database, cache, messaging, search, scheduling, and storage

Create the middleware register from [data-and-middleware-artifacts.md](data-and-middleware-artifacts.md). For every current or proposed middleware dependency, define purpose, feature IDs, product/version or unresolved decision, ownership, topology, contracts/data, consistency, security, capacity, failure/recovery, observability, and operations. Include a target deployment/topology diagram and per-feature interaction diagrams.

For caches, define source of truth, key/value/TTL, invalidation, staleness, fallback, security, capacity, and observability. For messaging/streaming, define contract reference, topology, delivery/ordering, publish coordination, idempotency, acknowledgement/offset, retry, dead-letter/quarantine, replay, security, capacity, and operations. Apply equivalent completeness to search, scheduler, object storage, and other middleware actually selected.

Use `cache-standard` and `message-standard` only when those technologies are selected. Load only the selected broker reference.

## 7. Server security and privacy

Define identity validation, server authorization and isolation, trust boundaries, data classification/protection, secrets/key boundaries, audit, abuse controls, privacy/retention/deletion, dependency/runtime security, control ownership, safe failure, verification, exceptions, and residual risks. Never delegate authoritative authorization to the client.

## 8. Error handling and resilience

Define internal error taxonomy, throw/result/catch/translation boundaries, cause preservation, terminal handling, retryability, single-owner logging, end-to-end deadlines, bounded retries, circuits, bulkheads, overload/load shedding, degradation, health, failover/failback, and integrity reconciliation.

Reference Integration SD for public error semantics.

## 9. Performance and capacity

Define measurable latency/throughput targets or labeled assumptions, workload/data model, budgets, bottlenecks, quotas, concurrency, headroom, scaling limits, dependency capacity, failover capacity, and required evidence.

## 10. Configuration, observability, and operations

Define configuration schema/source/precedence/validation/scope/refresh/drift/secret boundaries; logs/metrics/traces/audit and correlation; SLIs/SLOs, dashboards, alerts, diagnostics, ownership, runbooks, incidents, maintenance, support, and exercises. Keep statement-level instrumentation in SDD.

## 11. Deployment, release, and recovery

Define immutable artifact identity/provenance, environments/promotion, topology, compatibility, migration/configuration order, rollout/exposure, health/drain, rollback/roll-forward, backup/restore, disaster recovery, approvals, and post-release evidence. Reference Integration SD for mixed-version cross-boundary behavior.

## 12. Technology decisions and ADRs

Retain only material decisions with driver, selected decision, rationale, consequences, owner, and status. Record deferred material decisions explicitly; do not require a solution-comparison table.

## 13. Verification and handoff

Map requirement/SA IDs through feature/diagram, component/interface, data/DDL/DML/middleware decisions to unit/component, integration, contract, security, performance, resilience, migration, compatibility, and operational evidence. Record `Data-Ready` and `Middleware-Ready` when applicable, backend implementation prerequisites, sequencing, risks, dependencies, residual limitations, and Backend-Ready recommendation.
