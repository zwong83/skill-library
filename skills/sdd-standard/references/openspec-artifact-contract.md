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

Consume approved technical decisions and supplied code/test evidence as data when mapping the design delta. Do not load implementation/testing workflows or implement/execute their guidance from this artifact workflow. Record module, API, data, security, resilience, middleware, frontend, diagnostics and delivery constraints by reference to their approved owners. Material missing decisions return to System Design or requirements; concrete code and test changes belong to independently invoked workflows.

Use `plantuml-syntax` only when a change-specific design-mapping diagram is needed; do not duplicate approved System Design views without reason.

Record concrete implementation contracts and verification intent in the design delta; keep statement-level placement and code edits in implementation tasks.

### Risks / Trade-offs

Identify failure modes, technical debt, operational risk, dependency risk, mitigations, owners, and verification evidence. Material unresolved risks block artifact readiness.

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
- use the comment and API documentation guidance in `clean-code-standard` when a public contract or non-obvious intent, invariant, concurrency constraint, security constraint, compatibility concern, algorithm, or workaround needs explanation;
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

OpenSpec's active schema may not define a Test Analysis artifact. When independently requested, Test Analysis may supply a test plan from approved requirements/design and change impact. Link the supplied artifact from a project-approved location; do not invoke its agent or require complete OpenSpec artifacts for that independent analysis.

The TA should contain source/change baseline, change-impact and risk registers, a complete Test Case Matrix with positive/negative/boundary and other applicable categories, exact oracles, unit/integration/contract/UI/system-E2E/performance/security/regression allocation, specialist prerequisites and expected outputs, data/environment/dependency/authorization needs, case-to-task-to-specialist mapping, coverage gaps, residual risk, and `TA-Ready` or `TA-Blocked` status.

Label this file as a supplemental extension when it is not part of the active OpenSpec schema. Do not include it in `applyRequires` or claim OpenSpec validation covers it unless the observed schema explicitly does so.

## Supplemental specialist test evidence

When the project has no established evidence system, the applicable test specialists may place `unit-test-evidence.md`, `integration-test-evidence.md`, `contract-test-report.md`, `ui-test-report.md`, `system-e2e-test-report.md`, `performance-test-report.md`, `security-test-report.md`, or `regression-test-report.md` in the change directory or another approved location. Create only reports required by the applicable test plan or project; retained CI/tool artifacts may be referenced instead of duplicating them.

Each report must identify source/case IDs and supplied TA IDs when available, baseline and environment, exact execution or review evidence, results, failures/skips/flakiness, limitations, residual risk, and owning specialist. UI and performance reports additionally retain their governed visual/accessibility or workload/capacity evidence; the regression report records selected/excluded suites and its unified verdict.

Treat these files as supplemental extensions unless the observed schema defines them. Do not include them in `applyRequires`, claim OpenSpec validation covers their contents, or use them to override failed underlying evidence.
