# OpenSpec Artifact Contract for SDD

OpenSpec's active schema, instructions, and templates govern file names and required structure. This contract defines the semantic content and lifecycle boundaries expected by `sdd-standard`.

## Proposal

The proposal defines the current change and its source baseline.

### Source baseline

Identify the approved BRD/PRD/SRS/FRS/SA/Change Request sources and the SD Index plus applicable Backend/Frontend/Integration/contract artifacts that authorize the change, including versions and statuses. Add this section when the active template does not already provide an equivalent location.

### Why

Explain the concrete problem, motivation, desired outcome, and why the change is needed now. Reference the upstream requirement or design driver; do not recreate the complete business case.

### What Changes

Describe externally visible behavior changes, implementation-significant changes, removals, and explicitly unchanged behavior. Keep the boundary precise enough to detect scope creep.

### Capabilities

List new capability identifiers and modified existing capabilities. A modified capability belongs here only when its requirements or observable behavior change, not for an implementation-only refactor.

### Impact

Identify affected applications, components, APIs, events, data, dependencies, users, operations, migrations, compatibility, rollout, and documentation. State cross-repository ownership when relevant.

### Out of scope

List intentionally excluded behavior and follow-up work. Add this section when needed to prevent ambiguity.

## Capability delta specs

Use one spec per capability as directed by OpenSpec. Use the active schema's accepted delta headings, normally including `ADDED`, `MODIFIED`, `REMOVED`, or `RENAMED` requirements as applicable.

For every requirement:

- use a stable requirement ID when the project convention supports IDs;
- state one observable, normative behavior;
- identify its upstream source and acceptance relationship;
- avoid implementation detail unless it is itself a required constraint;
- define at least one scenario using the active OpenSpec syntax;
- cover success, validation, authorization, failure, edge, state-transition, concurrency, and recovery behavior when applicable;
- include measurable NFR thresholds when the requirement depends on them.

A scenario should establish precondition/event and expected outcome. Do not use vague results such as “works correctly,” “handles errors,” or “is performant.”

For modified requirements, preserve the complete intended requirement after the change rather than documenting only an ambiguous fragment. For removals and renames, include compatibility, migration, and consumer impact where applicable.

## Design delta

The OpenSpec design is subordinate to and traceable to the approved System Design set. It records how this change will be realized, not a replacement architecture document.

### System Design inheritance and escalation gate

Load the SD Index and only the affected Backend/Frontend/Integration sections and contract artifacts. Classify every implementation-design item before recording it:

| Classification | SDD action |
|---|---|
| Approved SD decision | Inherit it as a constraint, cite the decision, and map it to concrete implementation and verification without reopening the choice. |
| Implementation detail within approved SD boundaries | Refine it in the OpenSpec design delta, explain the mapping, and keep it consistent with the applicable approved authority and project conventions. |
| Material design change | Stop. Update and approve the affected Backend, Frontend, Integration, contract, and Index artifacts first, then revise the OpenSpec design and tasks before implementation. |

A material design change includes selecting or changing architecture/paradigm, module or layer boundaries, dependency direction, public interfaces, data ownership, transaction/consistency boundaries, security posture or control architecture, cache/messaging strategy, major error/recovery behavior, deployment topology, observability strategy, or frontend rendering/module/state ownership, supported-platform/accessibility commitment, performance/security posture, or build/delivery strategy. Do not disguise such a change as implementation detail.

### Context

Summarize the relevant current state, affected SD decisions, constraints, and existing implementation boundaries.

### Goals / Non-Goals

Define the technical outcomes this change must achieve and the design work intentionally excluded.

### Decisions

For each material decision, state:

- decision ID and related requirement/scenario IDs;
- selected approach and affected components;
- alternatives considered;
- rationale and trade-offs;
- interface, data, state, concurrency, error, and lifecycle behavior;
- security/privacy and trust-boundary impact;
- performance, reliability, observability, deployment, migration, rollback, and compatibility implications as applicable;
- approval status.

Use specialized skills in SDD as implementation-mapping and conformance references, not as permission to reselect the approved System Design. If a required material decision is absent or the implementation cannot conform, block and escalate to SD.

- Invoke `object-oriented-design`, `solid-principles`, and `design-patterns` only to map or verify an approved object/module/pattern direction into concrete class, interface, protocol, responsibility, identity/value, relationship, ownership, lifecycle, dependency, and collaboration details. A new material paradigm or pattern decision belongs in SD. Do not force these abstractions onto a clearer language-native implementation.
- Invoke `backend-layered-architecture-standard` only to map or verify approved module/layer boundaries, dependency direction, ports/adapters, transactions, composition, and test seams. Any material boundary or ownership change belongs in SD.
- Invoke `backend-api-design-standard` only to map or verify approved protocol, operations, schemas, authorization boundaries, errors, idempotency, pagination, limits, compatibility, and deprecation into framework code and contract tests. A material public or internal contract change belongs in SD.
- Invoke `backend-database-persistence-standard` only to map or verify approved datastore, ownership, schema, constraints, access paths, transactions, isolation, migrations, retention, and recovery into concrete persistence code and tests. A material ownership, datastore, invariant, or consistency change belongs in SD.
- Invoke `backend-resilience-standard` only to map or verify approved deadlines, retries, isolation, overload, degradation, health, reconciliation, failover, and recovery into concrete policies, configuration, telemetry, runbooks, and tests. A material failure or recovery strategy change belongs in SD.
- Invoke `backend-configuration-management-standard` only to map or verify approved schemas, sources, precedence, validation, refresh, secret boundaries, feature controls, drift, and failure behavior. A material configuration or secret-management policy change belongs in SD.
- Invoke `backend-performance-capacity-standard` only to map or verify approved objectives, workload assumptions, budgets, capacity, scaling, thresholds, and performance evidence. A material objective, topology, or capacity-strategy change belongs in SD.
- Invoke `deployment-release-standard` only to map or verify approved artifacts, environments, compatibility, rollout/release, migration, health, rollback/roll-forward, and evidence. A material deployment or release strategy change belongs in SD, and artifact design never authorizes a live release.
- Invoke `backend-operability-standard` only to map or verify approved ownership, SLIs/SLOs, dashboards, alerts, diagnostics, runbooks, incidents, maintenance, support, and readiness evidence. New support commitments or material health/operations policy belongs in SD.
- Invoke `testing-strategy-standard` only to map or verify approved risk coverage, levels/types, environments, data, automation, non-functional tests, gates, traceability, and evidence. Missing acceptance behavior or material risk-coverage changes belong in the owning requirements or SD artifact.
- Invoke `software-security-standard`, `backend-error-handling-standard`, `backend-caching-standard`, and `backend-messaging-standard` only to implement and verify approved security, failure, cache, and messaging decisions. Concrete types, keys, schemas, TTLs, mappings, retry parameters, topics/queues, acknowledgements, idempotency, dead-letter, replay, and test behavior may be refined within approved constraints; a strategy or posture change belongs in SD.
- Invoke `logging-standard` and `tracing-standard` only to convert approved observability contracts into concrete events, fields, severity, redaction, span boundaries, propagation, sampling, correlation, and tests. A material change to observability strategy belongs in SD.
- Invoke `frontend-architecture-standard`, `frontend-component-design-standard`, `frontend-state-data-standard`, `frontend-experience-standard`, `frontend-performance-standard`, `frontend-security-standard`, `frontend-observability-standard`, and `frontend-build-delivery-standard` only to map approved frontend SD decisions and the `Contract-Ready` interface into concrete routes, modules, components, state/data flows, UI states, budgets, controls, telemetry, artifacts, and tests. Material rendering/module/state ownership, public contract, security posture, support commitment, performance target, observability, or delivery-strategy changes belong in SD.
- Invoke `plantuml-syntax` before creating PlantUML only when an implementation-delta diagram materially clarifies the approved design mapping. Do not duplicate SD diagrams without a change-specific reason.

Record concrete implementation contracts and verification intent in the design delta; keep statement-level placement and code edits in implementation tasks.

### Risks / Trade-offs

Identify failure modes, technical debt, operational risk, dependency risk, mitigations, owners, and verification evidence. Material unresolved risks block apply readiness.

### Verification approach

Map each design-sensitive requirement to its required unit, integration, contract, end-to-end, security, performance, migration, or operational verification. Add this section when the template does not provide an equivalent.

## Tasks

Tasks translate approved specs and design into ordered, bounded work.

Every task must:

- use the active OpenSpec checkbox and numbering format;
- identify its requirement/scenario and design dependencies;
- name the expected implementation or artifact outcome without inventing file paths that have not been verified;
- include required tests or other evidence;
- include migration, documentation, observability, rollout, rollback, and cleanup work when applicable;
- apply `clean-code-standard` to production-code writing/refactoring and include naming, function/control-flow, nullability, side-effect, resource-lifecycle, and project-standard verification where applicable;
- include `code-comments` work only for public contracts or non-obvious intent, invariants, concurrency, security, compatibility, algorithms, and workarounds; do not add a task to narrate obvious code;
- be small enough to implement and verify without hiding unrelated changes;
- respect dependency order.

Do not mark a task complete when code exists but its required tests, migration checks, documentation, or operational evidence are incomplete.

## Supplemental verification evidence

OpenSpec's default `spec-driven` schema may not define a verification artifact. If the project has no existing evidence location, `sdd-standard` may add `verification.md` within the change directory as a clearly labeled extension. It should contain:

- source and artifact versions reviewed;
- requirement-to-evidence coverage matrix;
- commands/checks executed and results;
- manual verification and reviewer evidence;
- deviations and their disposition;
- convergence verdict, reviewer, and date.

Do not claim that this supplemental file is a built-in OpenSpec artifact, and do not use it to bypass the active schema's validation or project approval process.

## Supplemental Test Analysis

OpenSpec's active schema may not define a Test Analysis artifact. For behavior-changing work, `test-analysis-agent` may add `test-analysis.md` within the change directory or another project-approved evidence location after apply-required artifacts are complete.

The TA should contain source/change baseline, change-impact and risk registers, a complete Test Case Matrix with positive/negative/boundary and other applicable categories, exact oracles, unit/integration/contract/UI/system-E2E/performance/security/regression allocation, specialist prerequisites and expected outputs, data/environment/dependency/authorization needs, case-to-task-to-specialist mapping, coverage gaps, residual risk, and `TA-Ready` or `TA-Blocked` status.

Label this file as a supplemental extension when it is not part of the active OpenSpec schema. Do not include it in `applyRequires` or claim OpenSpec validation covers it unless the observed schema explicitly does so.

## Supplemental specialist test evidence

When the project has no established evidence system, the applicable test specialists may place `unit-test-evidence.md`, `integration-test-evidence.md`, `contract-test-report.md`, `ui-test-report.md`, `system-e2e-test-report.md`, `performance-test-report.md`, `security-test-report.md`, or `regression-test-report.md` in the change directory or another approved location. Create only the reports required by the TA and project; retained CI/tool artifacts may be referenced instead of duplicating them.

Each report must identify source/TA case IDs, baseline and environment, exact execution or review evidence, results, failures/skips/flakiness, limitations, residual risk, and owning specialist. UI and performance reports additionally retain their governed visual/accessibility or workload/capacity evidence; the regression report records selected/excluded suites and its unified verdict.

Treat these files as supplemental extensions unless the observed schema defines them. Do not include them in `applyRequires`, claim OpenSpec validation covers their contents, or use them to override failed underlying evidence.
