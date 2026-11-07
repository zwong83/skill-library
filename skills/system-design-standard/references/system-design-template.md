# System Design Template

Adapt this structure to the system and release. Keep unknowns explicit as `TBC`, `Proposed`, `Assumption`, `Pending Approval`, `Open`, or `Deferred`; do not turn a design assumption into an approved decision.

## Diagram-first rule

Use focused PlantUML diagrams as the primary views for architecture, component relationships, technical flows, state, data ownership, trust boundaries, and deployment. Use text as the normative source for contracts, rules, constraints, assumptions, exceptions, decisions, NFR targets, operational procedures, and unresolved items. Every diagram must have a title, scope, design explanation, and traceability.

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

Prefer a C4 context diagram to show users, external systems, system boundaries, trust boundaries, and major relationships. Explain ownership and assumptions in text.

### Container or subsystem view

Prefer a C4 container diagram to show the major applications, services, stores, and communication relationships. Keep responsibilities and design decisions in text.

### Responsibility and ownership map

Use a component or responsibility diagram when relationships are complex; use text to define ownership, lifecycle, and decision rationale.

### Trust boundaries and data classification

## 3. Component and Responsibility Design

Define components or modules, their responsibilities, dependencies, ownership, lifecycle, and communication patterns.

### Layer, module, and dependency design

When internal boundaries are material, define logical layers or feature modules, allowed and forbidden dependencies, ports/adapters, composition root, transaction and failure ownership, and enforcement strategy. Use `layered-architecture-standard`; do not force a fixed number of layers.

### Object-oriented design view (conditional)

When the selected implementation paradigm is object-oriented or hybrid, identify the high-level domain objects/modules, responsibilities, identities versus values, ownership, lifecycle, major relationships, dependency direction, and stable contracts needed for architecture review. Use `object-oriented-design` for this view. Keep detailed classes, methods, constructors, fields, and framework wiring in the downstream SDD/OpenSpec design.

### Component register

Prefer a C4 component or component diagram to show dependencies and boundaries. Keep each component's contract and rationale in text.

### Component detail template

#### `<Component name>`

##### Purpose and responsibilities

##### Inputs, outputs, and dependencies

Use a focused component, sequence, or data-flow diagram when interactions are complex. Define the authoritative contract and dependency rules in text.

##### State and lifecycle

##### Failure behavior and recovery

##### Security and data access

##### Observability and operations

##### Scaling and performance considerations

##### Alternatives and rationale

## 4. Interface and Contract Design

Specify the interfaces required for implementation and integration review. Keep contracts consistent with the source requirements and business behavior.

Use `api-design-standard` for applicable HTTP, gRPC, GraphQL, or internal service APIs. The System Design owns protocol and operation semantics, schemas, authorization boundaries, idempotency, compatibility, limits, deprecation, and failure behavior; SDD owns concrete framework mappings.

### Interface inventory

Use an interface or component view to show ownership and relationship. Keep the detailed contract, validation, errors, and compatibility rules in text.

### API or service contract template

#### `<Interface name>`

##### Purpose and ownership

##### Operations and message model

##### Request/response or event contract

##### Authentication and authorization

##### Validation and error model

Define stable error categories/codes, throw-or-return expectations, translation boundaries, safe public exposure, retryability, terminal handling, and logging ownership. Use `error-handling-standard` when errors cross components or protocols.

##### Idempotency, retries, timeouts, and rate limits

##### Versioning and compatibility

##### Monitoring and reconciliation

## 5. Data Architecture and Persistence Design

Define data ownership, logical/physical structures, consistency, lifecycle, privacy, retention, migration, backup, and recovery.

Use `database-persistence-standard` when durable state is introduced or changed. The System Design owns datastore and data ownership, invariants, schemas, access paths, transactions, isolation, migration strategy, retention, and recovery objectives; SDD owns concrete mappings, migrations, queries, settings, and tests.

### Data ownership and source of truth

### Logical data model

Prefer an ER or class diagram for entities, relationships, cardinality, and ownership. Define constraints, lifecycle, privacy, and consistency in text.

### Physical schema or storage model

### Consistency and transaction boundaries

### Indexing, partitioning, and capacity assumptions

### Retention, deletion, privacy, and access control

### Migration, backup, restore, and recovery

### Caching design (conditional)

When caching is justified, use `caching-standard` to define the measurable objective, source of truth, placement/pattern, key/value contract, tolerated staleness, TTL/refresh, invalidation ownership, failure/fallback behavior, tenant/security boundary, capacity, and observability. Keep concrete keys and configuration in SDD.

## 6. Interaction, Sequence, and State Design

Show how components collaborate across critical flows, including success, failure, retry, timeout, and recovery paths.

### Critical sequence diagrams

Use sequence diagrams as the primary view for cross-component timing, calls, messages, retries, and failure paths. Explain timeout and compensation rules in text.

### State machine design

Use state diagrams as the primary view for lifecycle states and transition guards. Define state meaning, side effects, authorization, and exceptions in text.

### Data-flow and event-flow design

Use data-flow or sequence diagrams to show movement, transformation, and ownership of data. Keep schemas, retention, privacy, and consistency rules in text.

### Messaging and event-stream design (conditional)

When asynchronous messaging is used, apply `messaging-standard` to define message purpose/ownership, contract/versioning, broker choice, topology, delivery and ordering scope, publish coordination, consumer idempotency, acknowledgement/offset point, retry, dead-letter/quarantine, replay, security, capacity, and operations. Load only the selected broker reference.

### Concurrency and ordering behavior

### Timeout, retry, and compensation behavior

## 7. Security and Privacy Design

Translate approved security and privacy requirements into enforceable design controls and review evidence.

Use `software-security-standard` in System Design mode. Include a security context and trust/data-flow view, threat and abuse-case register, control-ownership matrix, access-control matrix, data-protection and key/secret decisions, safe failure/audit behavior, operational controls, verification matrix, and residual risks where applicable. Do not invent policy, compliance, algorithms, vendors, or approval.

### Identity and authentication

### Authorization and tenant/data isolation

### Secrets and key management

### Data protection in transit and at rest

### Audit, threat considerations, and abuse controls

### Privacy, retention, and deletion controls

## 8. Reliability, Performance, and Scalability Design

Show how the design meets quality targets under normal load, degraded operation, and recovery conditions.

Use `resilience-standard` to define end-to-end deadlines, retry ownership and budgets, idempotency dependencies, isolation, overload controls, degraded modes, health semantics, reconciliation, failover, failback, and recovery. Keep thresholds tied to approved targets or clearly labeled assumptions.

Use `performance-capacity-standard` to define measurable latency/throughput objectives, workload and data models, end-to-end budgets, bottleneck evidence, headroom, quotas, scaling, failover capacity, and required performance tests.

### Performance model and capacity assumptions

### Availability and failure domains

### Scalability and load distribution

### Resilience, fallback, and disaster recovery

### Consistency, reconciliation, and data integrity

## 9. Observability and Operations Design

Define how the system will be monitored, operated, supported, diagnosed, and changed safely.

Use `operability-standard` for ownership, SLIs/SLOs, operational questions, dashboards, alerts, diagnostics, runbooks, incidents, maintenance, support, drills, and readiness evidence.

### Logs, metrics, traces, and audit events

Define the operational questions, event/span ownership, cross-service or asynchronous trace topology, context propagation, correlation, security/audit requirements, sensitive-data exclusions, sampling, retention, access, and cost controls. Use `logging-standard` and `tracing-standard` when these concerns are material. Keep code-level log statements and custom span placement in SDD/implementation.

### Alerts, dashboards, and escalation

### Runbooks and operational ownership

### Deployment, rollback, and configuration management

Prefer a deployment diagram for nodes, environments, trust boundaries, and dependencies. Define rollback, configuration ownership, and operational procedures in text.

Use `configuration-management-standard` for configuration schemas, source/precedence, validation, refresh, secret boundaries, feature controls, drift, change rollout, and failure behavior. Use `deployment-release-standard` for artifact provenance and promotion, environment gates, compatibility, rollout/release strategy, database/configuration sequencing, rollback/roll-forward, approvals, and evidence.

### Backup/restore and continuity validation

## 10. Technology Choices and Alternatives

Document approved or proposed technology choices with decision criteria and consequences. Do not present a proposal as an approval.

### Technology decision register

### Alternatives and trade-offs

### Cost, schedule, and operational impact

### Deferred technical decisions

## 11. Verification and Implementation Handoff

Define how the design will be verified and what implementation teams need before coding or deployment begins.

Use `testing-strategy-standard` to map requirements, design decisions, risks, and failure modes to the appropriate static, unit/component, integration, contract, system/end-to-end, acceptance, security, performance, resilience, migration, compatibility, and operational evidence.

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
