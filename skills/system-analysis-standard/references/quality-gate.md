# System Analysis Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`. Do not convert a gap into an invented design choice.

## Input readiness

- Mandatory task, system identity, and requirements baseline are present.
- Applicable FRS, Change Request, security/privacy, performance, integration, data-retention, availability, recovery, and operational inputs are supplied or explicitly marked `Not Applicable`.
- Optional research, examples, diagrams, logs, and benchmarks are not treated as blockers or approvals.

## Source and scope

- Governing source documents are identified with version/status.
- System purpose, boundaries, scope, exclusions, actors, and release context are explicit.
- Assumptions, constraints, dependencies, and analysis limitations are distinguished from confirmed facts.

## Logical decomposition

- Capabilities map to source requirements and do not overlap ambiguously.
- Actors, roles, permissions, responsibilities, and operational handoffs are explicit.
- Role-specific use-case diagrams are split by materially different responsibility boundaries rather than hidden in one panoramic diagram.
- Every upstream feature point appears in the reconciliation table with change type, disposition, owner/domain, target SA location, and status, including reused, deferred, deleted, and out-of-domain items.
- Important use cases include preconditions, triggers, main flow, alternate/exception paths, postconditions, and verification scenarios.
- Stateful concepts include logical permission/actor ownership, state diagram, and allowed-action/transition table. Validation, idempotency, concurrency, expiry, recovery, audit, and observability are analyzed where relevant.

## Diagram quality

- The feature inventory and diagram coverage matrix contains every in-scope feature and source ID.
- The full SA contains current context/main flow/problem views for brownfield scope, target context/main flow views, and a conceptual/logical data model where data is material.
- Every feature has a dedicated To-Be technical-logic activity or high-level sequence diagram; every changed brownfield feature also has an evidence-based As-Is path and problem IDs.
- Stateful, data-changing, and cross-boundary features have the applicable state, logical data, and integration views or an explicit source-based `Not Applicable` rationale.
- Each diagram has a title, scope, textual explanation, source traceability, and required legend or assumptions.
- Diagrams are readable and answer one clear question rather than combining unrelated concerns.
- Complex features are split into focused operation/logical-unit diagrams with cross-references, and material alternate/failure branches are shown.
- New/modified/removed notation is consistent and includes labels/legend rather than relying on color alone.
- Text is concise and adds only rules, constraints, exceptions, decisions, acceptance criteria, traceability, evidence, and unresolved items rather than repeating visual content.
- Diagram and text do not conflict; any conflict is recorded and resolved before approval.
- Diagram IDs resolve to maintained PlantUML sources; rendered previews are linked when rendering tooling is available, and any claimed syntax/render check has actual evidence.

## Data and integration analysis

- Logical data concepts have ownership, lifecycle, consistency, history, retention, privacy, and access implications.
- The logical data-operation matrix maps each data-affecting feature to create/read/update/delete/derive/publish behavior and source-of-truth ownership without leaking physical schemas into SA.
- Integrations have purpose, business data, timing, failure/fallback behavior, reconciliation, ownership, and approval status.
- Needed database/cache/queue/stream/search capabilities are visible at the logical level; products, DDL, DML, concrete schemas, cache keys, topics/queues, and deployment topology are deferred explicitly to SD.
- Source-of-truth responsibilities and cross-boundary failure effects are clear.

## Quality and risk analysis

- Performance, capacity, availability, reliability, security, privacy, accessibility, compatibility, observability, recovery, and compliance impacts are considered where applicable.
- Applicable assets, human/workload actors, trust boundaries, sensitive data, abuse cases, permission and isolation needs, audit expectations, and security acceptance outcomes are explicit enough for System Design; implementation mechanisms are not prematurely selected.
- Decisions have rationale, impact, status, and ownership; risks, dependencies, and open decisions have owners or next actions when known.

## Traceability and boundary

- Critical source requirements trace to capabilities/use cases, logical responsibilities, design inputs, and verification scenarios.
- The document does not silently include frameworks, physical schemas, endpoint contracts, class design, algorithms, deployment topology, or code.
- The handoff to System Design is explicit and complete enough to prevent design from guessing business behavior.

## Readiness

- Approval status and version history are present.
- Material unresolved scope, ownership, state, integration, security, or acceptance decisions are visible.
- The analysis is not called approved or design-ready while material decisions remain pending.
- The analysis is not called design-ready while any in-scope feature lacks mandatory diagram coverage.
- The readiness self-check links source reconciliation, diagram coverage, unresolved blockers, and quality-gate evidence.
