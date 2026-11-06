# System Design Template

Adapt this structure to the system and release. Keep unknowns explicit as `TBC`, `Proposed`, `Assumption`, `Pending Approval`, `Open`, or `Deferred`; do not turn a design assumption into an approved decision.

## Document control

Record system/project name, design version, status, date, author, owner, reviewers, target release, governing analysis/requirements, and approval status.

### Source baseline and design status

Record source versions, architecture drivers, confirmed constraints, unresolved decisions, design limitations, and the next review action.

## 1. Architecture Drivers and Design Principles

State the requirements, quality attributes, constraints, risks, cost/schedule factors, and principles that drive the design.

### Functional drivers

### Quality and operational drivers

### Constraints and assumptions

### Design principles and decision criteria

## 2. System Context and Architecture Overview

Show the system boundary, external actors, neighboring systems, major containers/components, trust boundaries, and the overall request/data flow.

### Context view

### Container or subsystem view

### Responsibility and ownership map

### Trust boundaries and data classification

## 3. Component and Responsibility Design

Define components or modules, their responsibilities, dependencies, ownership, lifecycle, and communication patterns.

### Component register

### Component detail template

#### `<Component name>`

##### Purpose and responsibilities

##### Inputs, outputs, and dependencies

##### State and lifecycle

##### Failure behavior and recovery

##### Security and data access

##### Observability and operations

##### Scaling and performance considerations

##### Alternatives and rationale

## 4. Interface and Contract Design

Specify the interfaces required for implementation and integration review. Keep contracts consistent with the source requirements and business behavior.

### Interface inventory

### API or service contract template

#### `<Interface name>`

##### Purpose and ownership

##### Operations and message model

##### Request/response or event contract

##### Authentication and authorization

##### Validation and error model

##### Idempotency, retries, timeouts, and rate limits

##### Versioning and compatibility

##### Monitoring and reconciliation

## 5. Data Architecture and Persistence Design

Define data ownership, logical/physical structures, consistency, lifecycle, privacy, retention, migration, backup, and recovery.

### Data ownership and source of truth

### Logical data model

### Physical schema or storage model

### Consistency and transaction boundaries

### Indexing, partitioning, and capacity assumptions

### Retention, deletion, privacy, and access control

### Migration, backup, restore, and recovery

## 6. Interaction, Sequence, and State Design

Show how components collaborate across critical flows, including success, failure, retry, timeout, and recovery paths.

### Critical sequence diagrams

### State machine design

### Data-flow and event-flow design

### Concurrency and ordering behavior

### Timeout, retry, and compensation behavior

## 7. Security and Privacy Design

Translate approved security and privacy requirements into enforceable design controls and review evidence.

### Identity and authentication

### Authorization and tenant/data isolation

### Secrets and key management

### Data protection in transit and at rest

### Audit, threat considerations, and abuse controls

### Privacy, retention, and deletion controls

## 8. Reliability, Performance, and Scalability Design

Show how the design meets quality targets under normal load, degraded operation, and recovery conditions.

### Performance model and capacity assumptions

### Availability and failure domains

### Scalability and load distribution

### Resilience, fallback, and disaster recovery

### Consistency, reconciliation, and data integrity

## 9. Observability and Operations Design

Define how the system will be monitored, operated, supported, diagnosed, and changed safely.

### Logs, metrics, traces, and audit events

### Alerts, dashboards, and escalation

### Runbooks and operational ownership

### Deployment, rollback, and configuration management

### Backup/restore and continuity validation

## 10. Technology Choices and Alternatives

Document approved or proposed technology choices with decision criteria and consequences. Do not present a proposal as an approval.

### Technology decision register

### Alternatives and trade-offs

### Cost, schedule, and operational impact

### Deferred technical decisions

## 11. Verification and Implementation Handoff

Define how the design will be verified and what implementation teams need before coding or deployment begins.

### Design acceptance criteria

### Requirement-to-design-to-test traceability

### Security and operational review checklist

### Implementation prerequisites and sequencing

### Approval and sign-off

## 12. Risks, Dependencies, and Change Control

Record design risks and govern changes that affect behavior, interfaces, data, security, operations, cost, or schedule.

### Risk register

### Dependency register

### Architecture decision records

### Version history and change-control rules

## Traceability

Maintain the critical path:

`Analysis requirement/flow -> Design decision/component/interface/data model -> Verification evidence`
