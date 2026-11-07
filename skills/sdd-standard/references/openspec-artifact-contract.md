# OpenSpec Artifact Contract for SDD

OpenSpec's active schema, instructions, and templates govern file names and required structure. This contract defines the semantic content and lifecycle boundaries expected by `sdd-standard`.

## Proposal

The proposal defines the current change and its source baseline.

### Source baseline

Identify the approved BRD/PRD/SRS/FRS/SA/SD/Change Request sources that authorize the change, including versions and statuses. Add this section when the active template does not already provide an equivalent location.

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

The OpenSpec design is subordinate to and traceable to the approved System Design. It records how this change will be realized, not a replacement architecture document.

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

Invoke `object-oriented-design` conditionally when an object-oriented or hybrid implementation needs detailed class/interface/protocol responsibilities, identities, values, relationships, ownership, lifecycle, dependency direction, or collaboration design. Invoke `solid-principles` conditionally to review that object/module design for responsibility, substitutability, consumer contracts, and dependency direction. Invoke `design-patterns` conditionally when a reusable pattern is selected or compared. Invoke `plantuml-syntax` before creating PlantUML diagrams. Do not force OOP, SOLID abstractions, patterns, or diagrams when a simpler language-native representation is clearer.

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
