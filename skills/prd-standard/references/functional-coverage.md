# Functional Coverage Through the Delivery Lifecycle

Use this reference for a full PRD, SA, or SD draft/review, or before declaring a delivery scope ready. For a bounded refinement, reconcile the changed requirements and material dependencies against the same baseline. Reuse the project's existing traceability artifact.

## Set the unit of coverage

A coverage row is an independently observable operation, state transition, or functional constraint. Split a broad requirement when its parts have different triggers, responsible actors or components, rules, outcomes, failure paths, or delivery timing. Derive roles and entry points from the actual system. A human actor, user interface, or particular channel is required only where the governing requirements call for one.

Preserve each BRD source ID, including functional obligations in rules, policies and acceptance criteria. Add a stable child ID when one source item contains several distinct behaviors. Record the obligation once and link to evidence at each stage:

| BRD ID | Function ID | Trigger, owner and observable result | PRD requirement and acceptance | SA logical path | SD realization and verification | Scope/status |
| --- | --- | --- | --- | --- | --- | --- |

Define the normal result and applicable validation, permission denial, stale state, failure and recovery. Derive supporting actions from the approved journey. Record any addition that changes business behavior or phase as a decision for the responsible owner.

## Reconcile source and release scope

1. Establish the complete functional inventory from the approved BRD, or from the explicitly authorized equivalent if the project does not use a BRD. Record the source version and approved scope. Use this same inventory for the PRD, SA and SD checks. A downstream artifact may narrow its delivery scope, but omissions in an intermediate document must remain visible in the inventory.
2. At each stage, reconcile every baseline row. Use `Covered`, `Gap`, `Needs decision`, `Deferred`, or `Not Applicable` with an evidence link, responsible owner or rationale as appropriate. A phase-limited artifact accounts for the rest of the baseline with the approved target phase or exclusion. Deferral does not count as designed coverage for that scope.
3. Read the linked evidence and verify the required behavior, conditions, outcomes and meaningful failure paths. A section, diagram, schema field or task heading alone cannot close a row. Trace new downstream behaviors back to authority so the check catches scope additions as well as omissions.
4. Resolve missing or contradictory requirements at their owning stage before the affected scope advances. Mark a stage ready only when all applicable functional obligations in its declared scope have evidence at that stage. Report full-BRD coverage separately from increment readiness. A candidate revision does not supersede approval or authorize implementation.

## Stage-specific evidence

| Stage | Evidence that closes the coverage row |
| --- | --- |
| PRD | Every functional obligation maps to a product requirement and observable acceptance, including applicable failures and recovery. The PRD links to the governing detail when the project maintains it in another approved requirements artifact. |
| SA | Logical owner, input and resulting state/effects, guards and exceptions, and the relevant path in a diagram and verification mapping. A focused diagram may cover related operations when each path is identifiable. |
| SD | Page/component or system entry, owned service action, authorization, expected results/errors, interface and persistence effects where applicable, and verification. Check contract fields and operations, state and DDL/DML, and UI loading/empty/error/recovery states against each other. |
| OpenSpec | Affected source/SD version, requirement and scenario IDs, and one or more tasks that implement and verify the behavior. Reconcile stale artifacts before test planning or Apply. |
| Test Analysis | Each in-scope operation maps to cases and observable oracles, allocated to suitable levels and linked to the implementation tasks. Missing or contradictory behavior returns to the owning source. |

Use versioned links and IDs to pass evidence forward. Keep rules and schemas in their owning artifacts. Additional SRS/FRS deliverables depend on the project's lifecycle. Where an equivalent is permitted, record the authorized owner, rationale, scope and exact artifacts. The coverage check still applies.

Report **semantic coverage**, **artifact validation**, and **approval/readiness** separately. Counts, valid links, document structure and OpenSpec strict validation cannot establish that every approved behavior was specified.
