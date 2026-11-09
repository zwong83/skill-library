# System Analysis Feature Diagram Coverage

Use this reference for every full System Analysis draft or review. The SA is a visual-first logical model: diagrams carry the primary explanation, while short tables and statements define the exact rules, exceptions, decisions, and unresolved items.

## Feature inventory and coverage matrix

Create one row for every in-scope feature or independently verifiable capability before drafting diagrams.

| Feature ID | Source IDs | Change type | Disposition/owner | As-Is flow | Problem IDs | To-Be logical flow | State view | Data view | Integration view | Status |
|---|---|---|---|---|---|---|---|---|---|---|

Every feature must have a dedicated To-Be logical-flow diagram. A shared journey diagram may cover multiple features only when each feature has a clearly labeled path and the matrix points to it; a generic system diagram is not sufficient feature coverage.

For brownfield work, every changed feature must also have an evidence-based As-Is flow and explicit problem markers. For greenfield work, mark As-Is and problem views `Not Applicable — greenfield` rather than inventing a current system.

## Required system-level views

For a full SA, include:

1. current system context and boundary view for brownfield scope;
2. current main end-to-end logical flow with failure, delay, manual, duplication, ownership, or visibility problems identified by stable issue IDs;
3. target system context and capability view;
4. target main end-to-end logical flow;
5. conceptual/logical domain and data-ownership model;
6. integration and trust-boundary view when any external boundary exists.

Keep As-Is and To-Be separate or use an unmistakable two-panel comparison. Never mix current facts and proposed behavior without labels.

## Required feature view

For each feature, include a compact feature analysis block containing:

- source requirement, actor, trigger, preconditions, postconditions, and owner;
- As-Is activity or high-level sequence for brownfield changes;
- problem-to-impact annotations linked to issue IDs;
- To-Be activity or high-level sequence showing responsibilities and decisions;
- alternate, failure, recovery, authorization, audit, and observable outcomes in the diagram when they materially change the flow;
- a state diagram when the feature changes lifecycle state;
- a conceptual data-flow or logical ER fragment when it creates, reads, updates, deletes, derives, or publishes material data;
- an integration sequence when responsibility crosses a system or trust boundary.

Do not require separate diagrams when one focused diagram can answer the same feature question legibly. Do not waive the dedicated To-Be technical-logic view.

## Sequence and change-view conventions

- Split complex features into focused diagrams per operation or logical unit and cross-reference them; do not create one panoramic sequence.
- Show all material alternate and failure branches with `alt`/`else`/`opt` or the equivalent activity branches.
- For change designs, mark new, modified, and removed participants/steps consistently. The default PlantUML palette is `#LightGreen` for new, `#Orange` for modified, and `#Pink` for removed, but always add labels/legend so meaning is not conveyed by color alone.
- Add a one-to-three-sentence caption stating the question answered, principal change, and any notation needed for review.
- Use one focused use-case diagram per materially different role; avoid a single mega-diagram.

## Visual notation routing

- Context/component view: system boundary, actors, external systems, ownership, trust boundaries.
- Use-case view: actor goals and feature relationships.
- Activity diagram: decisions, branches, parallel work, manual steps, and recovery.
- Sequence diagram: responsibility, timing, request/event order, and cross-boundary collaboration.
- State diagram: lifecycle, transition guards, terminal states, and recovery transitions.
- Logical ER/class view: concepts, relationships, cardinality, ownership, and lifecycle—not physical tables.

Invoke `plantuml-syntax` and load only the reference needed for the chosen diagram type.

## Text discipline

After each diagram, use only a compact companion table or bullets for:

- normative business rules and invariants;
- exceptions that cannot be represented clearly;
- assumptions and unresolved decisions;
- source and verification traceability;
- concise interpretation of the visual.

Avoid long prose that repeats diagram nodes and arrows. If a paragraph does not add a rule, constraint, exception, decision, evidence source, or unresolved item, remove it.

## SA boundary

SA owns conceptual/logical data models, ownership, lifecycle, and logical data operations. It may identify the need for a database, cache, queue, stream, search index, or other middleware capability, but it must not select a product or define physical tables, indexes, DDL, concrete DML, topics, queues, cache keys, or deployment topology. Those are System Design responsibilities.
