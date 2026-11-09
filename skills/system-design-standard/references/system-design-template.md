# System Design Document-Set Router

Use separate authoritative documents to prevent backend, frontend, integration, and coordination concerns from repeatedly loading one large SD.

## Required set

| Artifact | Required when | Authority |
|---|---|---|
| SD Index | Always | Sources, artifact versions, routing/status, readiness, unresolved items, review verdict, approvals |
| Backend SD | Backend/service/data/runtime behavior exists | Backend architecture, domain/data/transaction ownership, server controls, runtime quality, delivery, operations |
| Frontend SD | A frontend application exists | Rendering, routing, modules, components, state/data use, experience, client quality, frontend delivery |
| Integration SD | A cross-boundary contract exists | Boundary ownership, interaction semantics, errors, identity context, compatibility, contract verification |
| Machine-readable contracts | A protocol/schema benefits from executable structure | Field, message, operation, and protocol structure |
| Database design artifacts | Durable schema/access-path behavior is introduced or changed | Physical model, proposed DDL, DML/query catalog, transactions/concurrency, indexes, migration/backfill/recovery |

Load the Index template plus only the applicable design templates. A backend-only internal change may need Index and Backend SD; a UI-only change with an unchanged external contract may need Index and Frontend SD; a full product commonly needs all four.

## Shared document rules

- Adapt sections to scope; use `Not Applicable` with a short source-based rationale instead of loading an irrelevant specialist.
- Keep unknowns explicit as `TBC`, `Proposed`, `Assumption`, `Pending Approval`, `Open`, or `Deferred`.
- Use diagrams as the primary views. Every feature requires a dedicated target technical-flow diagram; brownfield changes also require current logic/problem views. Full designs include target architecture/main flow and applicable physical-data/middleware/deployment views.
- Keep text normative for decisions, contracts, rules, constraints, exceptions, targets, ownership, and procedures.
- Reference source IDs and other SD decision IDs instead of restating full upstream documents.
- Link to machine-readable contracts rather than reproducing their schema in Markdown.
- Link to authoritative `output/SD/database/` artifacts instead of duplicating full DDL or query catalogs in Backend SD.
- Record material decisions with rationale, consequences, owner, and status. Do not retain brainstorming or rejected-option lists.

## Conflict precedence

1. Approved requirements and System Analysis govern intended scope and behavior.
2. Machine-readable contract governs field/protocol structure.
3. Versioned database artifacts govern affected physical schema/DDL and the critical DML/query catalog.
4. Integration SD governs cross-boundary semantics.
5. Backend SD governs backend/data semantics, transactions, migration, recovery, internals, and server enforcement.
6. Frontend SD governs frontend internals and client behavior.
7. Index governs coverage, status, and readiness, not technical semantics.

Do not use precedence to hide a real contradiction. Record the conflict in `open-decisions.md`, resolve it with the owner, and update every affected authority before readiness.

## Minimal working state

Do not create specialist packet files, design-context, decision, conflict, routing, or review registers by default. The Index contains the small routing/status table and final review verdict. When material unresolved coordination remains, use only:

`output/SD/work/<project-name>/open-decisions.md`

Use columns: ID, decision needed, impact, owner, status, target document. Remove or archive resolved working state according to project convention.
