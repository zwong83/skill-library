# Functional Coverage Through the Delivery Lifecycle

Use this reference for a full product/system draft or review, when an agreed capability may have disappeared between stages, or before declaring an increment ready for implementation. For a bounded refinement, reconcile the changed operations and their material dependencies. Reuse the project's authoritative catalogue or coverage table.

## Set the unit of coverage

A coverage row is an independently observable actor or system operation, a material state transition, or a separately verifiable business constraint. Split a broad capability when its children have different actors, permissions, decisions, outcomes, failure/recovery paths, or release timing. Group related rows by actor and journey. Use a page, task surface, API, or background trigger as appropriate to the product. A label such as “manage catalogue” cannot establish coverage of its constituent operations.

Preserve existing source IDs. Add a stable operation ID when one source item contains several distinct actions. A useful compact catalogue records:

| Source ID | Operation ID | Actor and entry/trigger | Business rule and observable result | Acceptance IDs | Delivery and decision status |
| --- | --- | --- | --- | --- | --- |

Define the normal result and applicable validation, permission denial, stale state, failure and recovery. Derive supporting actions from the approved journey. Record any addition that changes business behavior or phase as a decision for the responsible owner.

## Reconcile source and release scope

1. Enumerate approved upstream actions and constraints before writing downstream rows. Map forward to the delivery artifact and backward to its authority. Cover operator setup, status/history, failure handling and handoffs when the source or flow requires them. Check both sides of a cross-role interaction.
2. Record each operation's disposition for the selected increment: `Covered`, `Gap`, `Needs decision`, `Deferred`, or `Not Applicable`. Give deferred or inapplicable items a phase or rationale and source. A shared commercial release capability can be deferred from the current build while still required for launch.
3. Inspect the referenced artifact, not just the existence of a link. A workflow, a diagram, an API field, or a task group title by itself does not prove the associated behavior is defined. For example, an existing attachment reference does not specify how an actor supplies, previews, replaces or removes a file. A configuration write does not cover a required view of affected records.
4. On a mismatch, correct the owning source first or record the exact unresolved question. Preserve approved scope and versions. A candidate revision does not silently supersede a signed baseline, widen an approved increment, or authorize implementation.

## Stage-specific evidence

| Stage | Evidence that closes the coverage row |
| --- | --- |
| PRD or governing FRS | Actor/trigger, required behavior, visible outcome, applicable failure/recovery and acceptance criteria. Put detailed rows in the approved requirements artifact, with a compact index in the PRD if details are elsewhere. |
| SA | Logical owner, input and resulting state/effects, guards and exceptions, and the relevant path in a diagram and verification mapping. A focused diagram may cover related operations when each path is identifiable. |
| SD | Page/component or system entry, owned service action, authorization, expected results/errors, interface and persistence effects where applicable, and verification. Check contract fields and operations, state and DDL/DML, and UI loading/empty/error/recovery states against each other. |
| OpenSpec | Affected source/SD version, requirement and scenario IDs, and one or more tasks that implement and verify the behavior. Reconcile stale artifacts before test planning or Apply. |
| Test Analysis | Each in-scope operation maps to cases and observable oracles, allocated to suitable levels and linked to the implementation tasks. Missing or contradictory behavior returns to the owning source. |

Use versioned links and IDs to pass evidence forward. Keep acceptance rules and schemas in their owning documents. Do not add separate SRS/FRS deliverables automatically to compensate for a sparse catalogue. Where the lifecycle permits an equivalent baseline, record the authorized owner, rationale, scope and exact artifacts. Missing requirements or controls remain gaps even if a separate document was waived.

Report **semantic coverage**, **artifact validation**, and **approval/readiness** separately. Counts, valid links, document structure and OpenSpec strict validation cannot establish that every approved behavior was specified.
