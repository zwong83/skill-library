# Integration System Design Template

Use this document for semantics crossing frontend/backend, service/service, event, batch, external-system, or trust boundaries. Reference machine-readable contracts for field/protocol structure; do not reproduce complete schemas.

## Required presentation order

After compact document-control metadata, the first technical content must be the overview diagram. Every substantive section below starts with its specified visual, then a short caption, then supplementary exact rules, rationale, constraints and evidence. This order is mandatory; do not start with narrative or a specification table. Reuse an authoritative diagram or focused excerpt when it already answers the section's question, with one maintained source. Embed a readable preview, or inline readable source with a rendering limitation when previews cannot be produced. A bare link or placeholder is insufficient. Use source-based `Not Applicable` only for truly unaffected sections; retain exact schemas/SQL and administrative records in their proper formats.

## Document control and boundary scope

Record version/status, owner, target release, participating systems/teams, source IDs, in/out of scope boundaries, linked Index/Backend/Frontend versions, and contract artifact versions/hashes.

## 1. Ownership and authority map

**Diagram first:** Present participant/ownership and trust-boundary diagrams. Follow with only the details the visuals cannot express precisely.

Define which participant owns domain rules, durable data, transactions, consistency, authorization enforcement, state transitions, errors, schema evolution, release compatibility, and operational response.

## 2. Contract inventory

**Diagram first:** Present a provider/consumer contract relationship diagram before the inventory. Follow with only the details the visuals cannot express precisely.

| Contract | Owner/provider | Consumers | Machine-readable path | Version/hash | Status |
|---|---|---|---|---|---|

Use only applicable OpenAPI, AsyncAPI, GraphQL, Protobuf, schema, or equivalent artifacts.

## 3. Interaction semantics

**Diagram first:** Present each crossing feature's target sequence/event-flow diagram, including material failure/recovery paths. Follow with only the details the visuals cannot express precisely.

For each feature that crosses a boundary, provide a dedicated target sequence/event-flow diagram and define purpose, participants, preconditions, business semantics, state effects, transaction/middleware boundary, sync/async behavior, success/failure/partial outcomes, and ownership. Brownfield changes also show or link the current boundary flow and problem IDs. A generic contract inventory does not replace per-feature interaction logic.

## 4. Identity, session, authorization, and trust

**Diagram first:** Present identity/session exchange, permission enforcement and safe-denial sequences. Follow with only the details the visuals cannot express precisely.

Define authentication/session exchange, caller/service identity, authorization context and result, tenant/data isolation, trust boundaries, credential/token handling responsibilities, audit correlation, and safe denial/failure. The server owns authoritative authorization.

## 5. Validation and error semantics

**Diagram first:** Present validation/error translation and correlation flows showing owning boundaries. Follow with only the details the visuals cannot express precisely.

Define validation ownership, stable public error categories/codes, safe details, retryability, terminal behavior, translation boundaries, correlation, and single-owner logging. Keep language/framework exception classes in SDD.

## 6. Idempotency, concurrency, and consistency

**Diagram first:** Present concurrency/idempotency/transaction and reconciliation sequences or state diagrams. Follow with only the details the visuals cannot express precisely.

Define idempotency scope/key/retention/result, duplicate and replay behavior, optimistic/pessimistic concurrency, version/conflict semantics, transaction boundaries, database/middleware participation, eventual consistency, reconciliation, compensation, and source of truth. Show material consistency and recovery paths in the applicable feature sequence.

## 7. Query, payload, and flow-control semantics

**Diagram first:** Present query/pagination or request/stream control-flow diagrams with applicable bounds, cancellation and backpressure. Follow with only the details the visuals cannot express precisely.

Define pagination, filtering, sorting, field selection, payload/rate/size limits, backpressure, deadlines/timeouts, cancellation, retry ownership/budgets, and overload/degraded behavior as applicable.

## 8. Compatibility and evolution

**Diagram first:** Present version/consumer dependency and rollout/migration/rollback sequences. Follow with only the details the visuals cannot express precisely.

Define versioning, additive/breaking change policy, deprecation, consumer/provider compatibility, mixed-version behavior, rollout order, migration/backfill, rollback/roll-forward, feature negotiation, and retirement evidence.

## 9. Examples, mocks, fixtures, and test contracts

**Diagram first:** Present a provider/consumer verification-boundary view tied to the relevant interaction before example/fixture references. Follow with only the details the visuals cannot express precisely.

Reference representative examples, mocks/fixtures, provider/consumer expectations, schema/protocol validation, contract tests, negative/boundary cases, compatibility matrix, and evidence owner. Avoid duplicating generated artifacts.

## 10. Frontend/backend contract readiness

**Diagram first:** Present a contract review/change/acceptance handoff diagram before version/status records. Follow with only the details the visuals cannot express precisely.

When frontend scope exists, record the backend domain/data/transaction/security ownership baseline, frontend journey review, accepted contract changes, unresolved unsupported UX needs, contract version/hash, and `Contract-Ready` status. Resolve excessive request fan-out, unstable client joins, duplicated business rules, ambiguous fields/errors, unsafe retries, and missing UI-state support before readiness.

## 11. Cross-boundary observability and operations

**Diagram first:** Present cross-boundary trace/event causality and incident ownership flows. Follow with only the details the visuals cannot express precisely.

Define correlation/trace propagation, async/middleware causality, audit identifiers, boundary SLIs/SLOs, dashboards/alerts, dependency ownership, diagnostics, incident handoff, reconciliation/runbooks, and support expectations. Link the authoritative middleware register/topology rather than duplicating it.

## 12. Verification and readiness

**Diagram first:** Present a cross-boundary verification/coverage view before evidence and readiness records. Follow with only the details the visuals cannot express precisely.

Map source and decision IDs to contract, integration, system/E2E, security, performance, resilience, compatibility, migration, and operational evidence. Record dependencies, residual risks, unresolved decisions, implementation prerequisites, and Integration-Ready recommendation.
