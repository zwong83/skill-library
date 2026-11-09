# System Analysis Template

Adapt this structure to the system and release. Keep unknowns explicit as `TBC`, `Proposed`, `Assumption`, `Pending Approval`, `Open`, or `Deferred`; do not fill analysis gaps with technical guesses.

## Visual-first rule

Use focused PlantUML diagrams as the primary views. Every feature requires a dedicated target logical-flow diagram; brownfield changes also require evidence-based current logic and problem views. Use short text/tables only for rules, constraints, exceptions, decisions, assumptions, acceptance criteria, and unresolved items. Every diagram must have a title, scope, concise explanation, and traceability.

## Construction order

Build the document in this order so reviewers can move from intent to current state, target behavior, feature detail, data/state, integration, quality, decisions, and handoff:

1. document control, terminology, requirement background, objectives, and source status;
2. current and target system context plus the current problems being solved;
3. actors/roles and role-specific use cases;
4. capability decomposition and feature-point reconciliation;
5. per-feature logical analysis blocks, which are the center of gravity;
6. domain/data/state analysis;
7. integration and logical middleware needs;
8. quality attributes, decisions, risks, dependencies, and open questions;
9. verification, readiness self-check, and System Design handoff.

Do not force irrelevant content merely to fill a heading. Keep the heading and record a short source-based `Not Applicable` rationale only when the project's document convention requires a stable skeleton.

## Document control

Record system/project name, analysis version, status, date, author, owner, reviewers, target release, governing sources, and approval status.

### Source documents and analysis status

Record source versions, confirmed decisions, assumptions, unresolved decisions, analysis limitations, and next review action.

### Terminology

List only terms, abbreviations, states, roles, and domain names used by this SA. Keep one canonical spelling per term.

### Requirement background and evidence

Summarize the current business/system problem without copying the BRD/PRD. Cite the source or current-system evidence for brownfield claims and link every problem to a stable problem ID.

### Business and analysis objectives

Separate expected business outcomes from the logical system outcomes this SA must establish. Preserve approved measurements; label missing targets rather than inventing numbers.

### Related documents

Link only confirmed BRD/PRD/SRS/FRS/Change Request, prior SA/SD, UX, policy, or evidence sources with version/status.

### Feature and diagram coverage

Use the matrix from [feature-diagram-coverage.md](feature-diagram-coverage.md). List every in-scope feature before drafting detail and keep coverage status current.

## 1. System Context and Scope

Explain the system's purpose, business or product context, system boundary, surrounding actors, and release boundary.

### Problem and desired system outcome

### System boundary

### In-scope capabilities

### Out-of-scope and deferred capabilities

### Context diagram

Required for a full SA. Show users, external systems, system boundaries, major information relationships, trust boundaries, ownership, and unresolved boundaries.

### Current system and problem view

For brownfield scope, show the current main flow and mark problem IDs at the exact step or boundary where delay, failure, duplication, manual work, missing ownership, poor visibility, or policy risk occurs. For greenfield scope, record `Not Applicable — greenfield`.

### Target system and main-flow view

Show the proposed target context and primary end-to-end logical flow. Link every changed responsibility to feature and source IDs.

## 2. Actors, Roles, and Responsibilities

Identify human users, external systems, operational roles, ownership, permissions, and responsibility boundaries.

### Actor register

| Actor/role | Human/system/operations | Goals | Responsibilities | Logical permission/decision needs | Source IDs |
|---|---|---|---|---|---|

### Role and permission model

Record logical permission/decision needs and responsibility boundaries; leave concrete permission codes and enforcement mechanisms to System Design unless they are already approved constraints.

### Role-specific use-case diagrams

Use one focused use-case diagram per materially different role or responsibility boundary. Avoid a panoramic mega-diagram that hides ownership.

### Responsibility allocation

### Operational ownership and handoffs

## 3. Capability Decomposition

Break the system into logical capabilities and show how they satisfy source requirements without selecting implementation components.

### Capability map

Prefer a capability or use-case view to show decomposition and relationships. Keep capability definitions and source IDs in text.

### Capability-to-requirement traceability

### Feature-point reconciliation

Map every upstream feature point to an SA feature ID and classify the change as `New`, `Contract`, `Logic`, `Deleted`, or `No Change`. Record disposition, owner/domain, target SA section/diagram, and status. No source feature may disappear because it is reused, deferred, deleted, or owned elsewhere.

| Source feature ID | Feature point | Change type | Disposition | Owner/domain | SA feature ID | Diagram/section | Status |
|---|---|---|---|---|---|---|---|

### Cross-cutting capabilities

## 4. Use Cases and User/System Flows

Describe the important end-to-end interactions and the system responsibilities in each path.

### Use-case and feature register

Use the role-specific diagrams from Section 2 and a register for feature/use-case IDs, source IDs, actor/owner, change type, priority, disposition, scope, and status.

### Per-feature logical analysis block

Repeat the following fixed structure for every in-scope feature. Split multiple operations or materially different branches into focused sub-diagrams with cross-references instead of creating one oversized diagram.

#### `<Feature ID — feature/use-case name>`

##### 1. Goal, source, change type, and ownership

Record source IDs, `New`/`Contract`/`Logic`/`Deleted`/`No Change`, actor, logical owner, trigger, preconditions, postconditions, and status.

##### 2. Current behavior and problem points

For a changed brownfield feature, provide or link the As-Is activity/sequence and locate problem IDs on the exact step or boundary. For greenfield scope, record `Not Applicable — greenfield`.

##### 3. Target logical flow

Required: provide a dedicated activity or high-level sequence diagram for this feature's To-Be technical logic. For a brownfield change, provide or link its As-Is path and problem markers. Use text only to define normative rules, conditions, and expected outcomes not clear in the visual.

Show applicable validation, authorization denial, alternate, exception, timeout, duplicate, concurrency, recovery, audit, and observable outcomes in the visual. Split complex logic into one diagram per operation/logical unit.

##### 4. Rules and decision table

Use a compact decision table for input/state combinations, rule outcome, forbidden effect, and source ID. Avoid narrative restatement of the diagram.

| Rule ID | Input/current state | Condition | Required outcome | Forbidden effect | Source ID |
|---|---|---|---|---|---|

##### 5. Exception and engineering-concern table

Record boundary condition, duplicate/idempotency concern, concurrency/expiry risk, recovery expectation, audit/observability outcome, and owner. Do not hide these concerns in a generic document-wide section.

| Concern ID | Trigger/condition | Expected behavior | Recovery/compensation | Audit/observable outcome | Owner |
|---|---|---|---|---|---|

##### 6. State, data, integration, and middleware impact

Link the applicable state view, logical data operations, cross-boundary sequence, and logical middleware capability need. Use `Not Applicable` with a reason for unaffected categories.

| Concern | Affected concept/boundary | Logical change | Owning view/diagram | SD decision required |
|---|---|---|---|---|

##### 7. Verification scenarios and SD inputs

Map expected outcomes and forbidden effects to verification scenarios, then list the exact technical decisions System Design must make.

| Verification ID | Preconditions/input | Expected outcome | Forbidden effect | Source/rule IDs | Required SD input |
|---|---|---|---|---|---|

## 5. Domain Concepts, Data, and State

Define logical concepts, ownership, lifecycle, state, consistency, history, and access boundaries.

### Domain concept model

Required when the system creates, reads, updates, deletes, derives, or publishes material data. Use a conceptual/logical ER or domain diagram with ownership and cardinality.

### Logical data ownership

Include a feature-to-data-operation matrix showing logical create/read/update/delete/derive/publish responsibilities and source of truth. Do not use physical table or SQL names.

### Entity lifecycle and state model

For every stateful concept, use a state triple: logical permission/actor ownership, state diagram, and `State | Meaning | Allowed actions/transitions | Guard/source` table. Define transition side effects, exceptions, terminal/recovery states, and ownership concisely.

### Data quality and consistency rules

### Audit, retention, privacy, and access implications

Do not include physical tables, indexes, DDL, or storage-engine choices here.

## 6. Integration and Interface Analysis

Analyze why integrations exist, what responsibilities cross the boundary, and how failures affect system behavior.

### Integration register

Use a context/component view for the integration landscape and a high-level sequence for every feature whose responsibility crosses a system or trust boundary. Identify logical middleware capability needs, but leave products and concrete topology to SD.

### Business-level data exchange

### Timing and sequencing expectations

### Failure, retry, fallback, and reconciliation

### Ownership and approval status

Leave endpoint contracts, authentication protocols, payload schemas, and implementation details to System Design.

## 7. Cross-Cutting Quality Analysis

Analyze how quality attributes affect system behavior and responsibilities without selecting implementation mechanisms.

### Performance and capacity implications

### Availability, reliability, and recovery

### Security, privacy, and authorization

When applicable, use `software-security-standard` in System Analysis mode to identify protected assets, actors and workload identities, trust boundaries, sensitive data, abuse cases, permission/isolation needs, audit expectations, security acceptance outcomes, and unresolved policy decisions. Keep algorithms, products, key stores, and concrete controls for System Design.

### Observability and supportability

### Accessibility, compatibility, and compliance

## 8. Analysis Decisions

Record only the selected logical decisions that System Design must honor, with source/driver, rationale, impact, owner, status, and affected feature/diagram IDs.

### Decision rationale and impact

Explain why each material decision satisfies the governing requirement or constraint and what it changes downstream. Do not add a solution-comparison table.

### Selected analysis direction

### Deferred decisions

### Decision register

## 9. Risks, Dependencies, and Open Questions

Make uncertainty visible before design begins.

### Risk register

### Dependency register

### Open question register

Centralize every `TBC`, `Pending Approval`, or `Open` item with affected feature/diagram, impact, owner, next action, and target resolution date/status. Do not scatter unresolved questions only in prose.

### Resolution owner and next action

## 10. Verification and Design Handoff

Show how the analysis will be validated and what inputs System Design must receive.

### Analysis acceptance criteria

### Requirement-to-analysis-to-verification traceability

### System Design input checklist

### Approval and sign-off

### Readiness self-check

Summarize source coverage, feature reconciliation, diagram coverage, unresolved blockers, and the SA quality-gate result with evidence locations.

## Traceability

Maintain the critical path:

`Source requirement -> Analysis capability/use case -> Logical responsibility/flow -> Design input -> Verification scenario`
