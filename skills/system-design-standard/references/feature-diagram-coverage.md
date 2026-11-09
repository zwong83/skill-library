# System Design Feature Diagram Coverage

Use this reference for every full System Design draft or readiness review. The SD set is visual-first: diagrams explain the architecture and technical logic; compact tables and normative statements define exact contracts, rules, parameters, failure behavior, and decisions.

## Feature design inventory

Create one row for every in-scope feature or independently deployable/verifiable behavior before specialist routing.

| Feature ID | Source/SA IDs | Owner | Current view | Problem IDs | Target technical flow | Component/data view | State view | Middleware view | Verification | Status |
|---|---|---|---|---|---|---|---|---|---|---|

Every feature must have a dedicated target technical-flow diagram. A shared end-to-end diagram may satisfy several rows only when each feature has a clearly labeled path, ownership, and traceable diagram ID. A generic architecture picture does not count as feature logic.

For brownfield change scope, every changed feature must also show the evidence-based current runtime path and the exact problem/hotspot being changed. For greenfield scope, mark current/problem views `Not Applicable — greenfield`.

## Required system-level views

A full SD set includes, as applicable:

1. current context/container/component and deployment/middleware topology for brownfield scope;
2. current main runtime flow with problem IDs at the responsible component, boundary, datastore, or middleware hop;
3. target context/container/component architecture;
4. target main end-to-end runtime sequence including major failure/recovery branches;
5. target deployment and middleware topology;
6. logical and physical data model plus ownership boundaries;
7. trust-boundary and control-enforcement view when security is material.

Keep As-Is and To-Be separate or use an unmistakable side-by-side comparison. Never depict a proposal as current fact.

## Required feature technical design block

For every feature, include:

- source and SA IDs, owner, entry point, preconditions, outputs, invariants, affected components/data/contracts, and verification intent;
- a target sequence or activity diagram showing concrete technical responsibility, calls/events, decisions, transaction boundaries, and observable outcome;
- success plus applicable validation, authorization denial, timeout, retry, duplicate, concurrency, partial-failure, compensation, fallback, and terminal behavior;
- a component/dependency or data-flow view when the feature spans modules or ownership boundaries;
- an As-Is sequence and problem markers for brownfield changes;
- a state diagram when lifecycle transitions are material;
- a data mutation/transaction diagram when durable state changes;
- a middleware interaction diagram when cache, queue, stream, search, scheduler, object storage, or another runtime dependency participates;
- a frontend route/component/state/data-flow view for each user-facing feature in Frontend SD.

Conditional views may be combined when the result remains readable. The dedicated target technical-flow diagram may not be omitted.

Use a consistent per-feature construction:

1. target technical sequence(s), split by operation/logical unit when needed;
2. engineering-constraint table for idempotency, concurrency, timeout, retry, consistency, security, and recovery traps;
3. interface/data/middleware impact table linking authoritative contracts and artifacts;
4. error/result table covering trigger, public/internal outcome, retryability, owner, and evidence.

Show material alternate/failure branches in the sequence. For change scope, mark new, modified, and removed participants/steps consistently; default to `#LightGreen`, `#Orange`, and `#Pink` with explicit labels/legend so color is never the only signal. Add a one-to-three-sentence caption and split oversized diagrams rather than reducing readability.

## Diagram identifiers and traceability

Give every diagram a stable ID such as `DIA-SYS-001`, `DIA-FEAT-ORD-001`, `DIA-DATA-001`, or `DIA-MW-001`. Each diagram records title, scope, As-Is/To-Be status, feature/source/decision IDs, owner, and assumptions/legend. The feature coverage matrix links diagram IDs, not copied diagrams.

Keep reusable PlantUML sources under `output/SD/diagrams/` when no project convention exists. Link the `.puml` source from the authoritative section and embed an SVG/PNG preview when rendering support exists. A generated image without maintained source is insufficient, and an unrendered source must not be reported as visually validated.

## Text discipline

After each diagram, include only compact design notes for exact rules, parameters, contracts, exceptions, security controls, NFR targets, unresolved decisions, and verification. Avoid prose that narrates arrows already visible in the diagram. Use tables for repetitive mappings and machine-readable artifacts for schemas.

## PlantUML routing

Invoke `plantuml-syntax` before authoring PlantUML. Use C4/context/component diagrams for architecture, sequence/activity for runtime logic, state for lifecycle, ER for data, and deployment/component diagrams for middleware and runtime topology. Load only the relevant syntax references.
