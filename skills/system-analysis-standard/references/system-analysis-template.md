# System Analysis Template

Adapt this structure to the system and release. Keep unknowns explicit as `TBC`, `Proposed`, `Assumption`, `Pending Approval`, `Open`, or `Deferred`; do not fill analysis gaps with technical guesses.

## Document control

Record system/project name, analysis version, status, date, author, owner, reviewers, target release, governing sources, and approval status.

### Source documents and analysis status

Record source versions, confirmed decisions, assumptions, unresolved decisions, analysis limitations, and next review action.

## 1. System Context and Scope

Explain the system's purpose, business or product context, system boundary, surrounding actors, and release boundary.

### Problem and desired system outcome

### System boundary

### In-scope capabilities

### Out-of-scope and deferred capabilities

### Context diagram

## 2. Actors, Roles, and Responsibilities

Identify human users, external systems, operational roles, ownership, permissions, and responsibility boundaries.

### Actor register

### Role and permission model

### Responsibility allocation

### Operational ownership and handoffs

## 3. Capability Decomposition

Break the system into logical capabilities and show how they satisfy source requirements without selecting implementation components.

### Capability map

### Capability-to-requirement traceability

### Cross-cutting capabilities

## 4. Use Cases and User/System Flows

Describe the important end-to-end interactions and the system responsibilities in each path.

### Use-case register

### Use-case template

#### `<Use-case name>`

##### Goal and source requirements

##### Actors and preconditions

##### Trigger and main flow

##### Alternate and exception flows

##### Authorization and validation

##### State changes and side effects

##### Idempotency, concurrency, and expiry

##### Recovery, audit, and observability

##### Postconditions and verification scenarios

## 5. Domain Concepts, Data, and State

Define logical concepts, ownership, lifecycle, state, consistency, history, and access boundaries.

### Domain concept model

### Logical data ownership

### Entity lifecycle and state model

### Data quality and consistency rules

### Audit, retention, privacy, and access implications

Do not include physical tables, indexes, DDL, or storage-engine choices here.

## 6. Integration and Interface Analysis

Analyze why integrations exist, what responsibilities cross the boundary, and how failures affect system behavior.

### Integration register

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

### Observability and supportability

### Accessibility, compatibility, and compliance

## 8. Alternatives and Analysis Decisions

Record meaningful alternatives, trade-offs, constraints, and decisions that design must honor.

### Option comparison

### Selected analysis direction

### Rejected or deferred options

### Decision register

## 9. Risks, Dependencies, and Open Questions

Make uncertainty visible before design begins.

### Risk register

### Dependency register

### Open question register

### Resolution owner and next action

## 10. Verification and Design Handoff

Show how the analysis will be validated and what inputs System Design must receive.

### Analysis acceptance criteria

### Requirement-to-analysis-to-verification traceability

### System Design input checklist

### Approval and sign-off

## Traceability

Maintain the critical path:

`Source requirement -> Analysis capability/use case -> Logical responsibility/flow -> Design input -> Verification scenario`
