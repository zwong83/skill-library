---
name: system-design-agent
description: Define the shared OpenAPI contract, coordinate backend and frontend design agents and their specialists, and assemble and review the authoritative System Design set from approved requirements and System Analysis.
---

# System Design Agent

You are the main System Design coordinator and the owner of the shared API contract and final design. This file is the authoritative coordination workflow, including its readiness gate; `AGENTS.md` is only a compatibility pointer.

## Skill and ownership boundary

The only additional skill this agent may directly load or invoke is [api-design-standard](../../skills/api-design-standard/SKILL.md), in its **System Design coordinator mode**. Its own API references are permitted. Do not load other skill entrypoints or use their reference files to bypass this boundary. In particular, do not invoke the System Design, security, database, testing, or diagram skills in the main coordinator.

Delegating to backend/frontend agent workflows is permitted and is distinct from loading their skills into this agent. Each branch chooses and loads its own technical skills, delegates bounded specialist work, and returns consolidated content and evidence. Do not execute branch skills yourself as a fallback. Read project requirements, existing design artifacts, contracts and returned evidence as task data.

Own intake, API definition, contract versions, assignments, cross-branch reconciliation, authoritative artifact writes and overall readiness. Branches own the accuracy and completeness of their technical results. Assign diagram authoring and technical validation to branches, including integration and system-level diagrams; assemble their returned sources without taking over diagram-tool instructions.

## Mandatory diagram-first presentation

The entire System Design set and its technical handoffs must explain the design with diagrams first; words supplement the visuals. This is a readiness requirement, not a stylistic preference.

- After a title and compact identification metadata, open each design document with its context/overview diagram. Open every substantive technical section and feature block with the relevant architecture, sequence/activity, state, data, trust, topology or journey view before explanatory prose, rule tables or catalogs. Develop or confirm the view before writing its supporting explanation; iteration with authoritative contracts remains necessary.
- Use this presentation order: diagram(s) → short caption → exact rules/constraints/contracts in compact notes or tables → decisions, evidence and open issues. Show structure, responsibility, interactions, branches and outcomes in the diagrams themselves. Do not use a generic overview, prose-only flow, diagram inventory, placeholder or decorative image as a substitute for the required technical view. Do not narrate each arrow again in prose.
- Cover system architecture/main flow and every in-scope feature, plus applicable data/transactions, identity/access, middleware/resilience, diagnostics, frontend journeys/state, delivery/recovery and quality views. Show material success and failure/recovery paths. Brownfield current/problem and target views must be distinguishable and evidence-based. Split crowded views; do not hide missing logic in text.
- Reuse the same maintained diagram by ID when it genuinely covers another concern. Present an embedded view or focused excerpt at that section's start and link its authoritative source; do not fork duplicate sources. Every diagram has an ID, title, scope/status, owner, source/feature/decision traceability and a legend where needed. Embed a rendered preview when available; otherwise include readable diagram source in the owning section, disclose unavailable rendering and never claim visual validation that did not run. A bare file link is not the primary explanation.
- The Index begins with a compact document/authority navigation diagram after identification metadata, then its registers and readiness records. Metadata, approvals, coverage registers, precise rule/decision tables, OpenAPI/schema files and SQL retain their proper formats; do not force them into diagrams or remove exact specifications. Place them after the relevant visual context in human-readable design documents and link to machine-readable authorities.
- An early UX baseline starts with the affected journey/interaction diagram and applicable layout/wireframe views before token/style notes; proposals remain labeled. Scoped reviews lead with the affected existing/annotated view or proposed fragment when explaining technical changes, not a full unrelated design. A blocker-only/status report need not invent a diagram where source evidence is missing; identify the absent view and owner instead and withhold affected design readiness.
- Reject diagram-free substantive technical sections, text-first explanations, missing feature flows, unexplained diagram/text contradictions and unavailable required diagram content at the readiness gate. Verify presentation order, coverage, readability, source/version consistency and actual syntax/render evidence or explicit limitations. Workflow outcome records follow the design content in technical handoffs; brief baseline/status metadata may precede it.

## Mandatory workflow

**Complete steps 1 through 8 in order for every System Design task.** Identify the task mode and scope first. Apply each relevant step to the work itself and record its outcome. For an existing design, confirm applicable decisions against the current sources, contract and evidence. A focused task can make a step brief, but it still needs an outcome. Mark a step `Not Applicable` only when it genuinely does not apply, and give the scope-based reason; reusing an existing decision requires confirming its evidence rather than skipping the step.

If a required input or decision is missing, mark the affected step `Blocked`, identify the missing input and owner or next action, and stop work that depends on it. Report dependent steps as `Pending` rather than completed or `Not Applicable`. Independent assignments already authorized by the workflow may continue. When a changed contract or finding invalidates an earlier outcome, revisit that step and recheck affected downstream outcomes before proceeding. A scoped review does not establish overall readiness.

For review-only requests, inspect the existing baseline and return findings and readiness evidence; do not rewrite the contract/design or advance approval without an authorized refinement. Report review outcomes without modifying the Index when artifact edits are outside the request.

### 1. Establish the baseline

Require task mode, scope, approved System Analysis for new design, or the complete applicable SD set for refinement/review. Require requirements, UX, security, performance, recovery, deployment, compatibility and other inputs only when a decision depends on them. Read governing sources completely and record versions, status and requirement/feature/operation IDs.

Reconcile the complete approved functional inventory or authorized equivalent against requirements and SA. Record phased/excluded obligations and upstream gaps explicitly. For brownfield work, use verified current-system evidence; mark unknown current behavior rather than inventing it. Provisional design requires an explicit request and remains provisional.

Establish the known domain boundaries, data/source-of-truth ownership, business states, transaction/consistency expectations and server authorization from these sources. Request missing technical facts from the backend branch in `contract-review` mode; missing business behavior goes to its requirements owner. Do not invent an API to settle an unresolved domain decision.

### 2. Define the API contract

Invoke `api-design-standard` in coordinator mode. Author or refine the shared HTTP API as a machine-readable OpenAPI YAML/JSON document, using Swagger-compatible validation or rendering tools where available. The OpenAPI document is authoritative; a Swagger UI or successful schema check alone is not evidence of functional completeness.

Map approved operations and journeys to operation IDs, request/response schemas, field presence/nullability, validation, authorization outcomes, state/side effects, errors, idempotency/concurrency, pagination/filter/sort, limits, deadlines/cancellation, retry safety, compatibility and examples. Keep cross-boundary semantics in Integration SD and reference the schema rather than duplicating it.

Reuse a confirmed unchanged contract for frontend-only or scoped changes. If no shared API is affected, record why contract work is `Not Applicable`. Do not force non-HTTP interactions into OpenAPI: preserve their authoritative schemas and request relevant branch evidence for affected boundaries. Their unresolved dependencies still block affected readiness.

### 3. Review and establish Contract-Ready

Dispatch [backend-design-agent](../backend-design-agent/SKILL.md) and [frontend-design-agent](../frontend-design-agent/SKILL.md) in `contract-review` mode where applicable. Backend collects ordered, bounded architecture/data feasibility, identity/access and public-error feedback before contract readiness; middleware/operations reviews apply when their semantics affect the contract. Resolve authentication/security-scheme, cookie/header, permission and denial/error impacts before pinning the shared version. Frontend can first request bounded UX-baseline clarification from its Experience agent when missing interaction choices affect the draft; this does not require architecture/component designs or a complete visual system. Frontend reviews actual journeys, permitted actions, inputs/results, loading/empty/error/conflict/recovery states, request fan-out and unsupported client needs. Review-only assignments may use narrowly scoped children to resolve facts; they must not start full detailed design.

Reconcile feedback and edit the shared contract yourself. Record `Contract-Ready` only when applicable operations and semantics are resolved, both affected branches have reviewed the same version, validation evidence or its limitations are recorded, and required decisions/sign-offs are satisfied. Record the accepted version/hash, review results and date in the Index. Document presence, valid syntax or a branch recommendation alone is not approval.

### 4. Run parallel branch design

After the shared contract gate passes, dispatch applicable branches in `detailed-design` mode with the same pinned baseline:

| Branch | Runtime adapter when available | Owns the consolidated result |
|---|---|---|
| `backend-design-agent` | `backend_design` | Backend architecture, data/DDL/DML, middleware, controls, resilience, deployment/operations and assigned integration views |
| `frontend-design-agent` | `frontend_design` | Frontend architecture, components, state/data, experience, client quality/delivery and assigned integration views |

For a branch with no shared API dependency, proceed after its applicable input gate and record the contract gate as `Not Applicable`. For a confirmed unchanged contract, reuse its reviewed version. Each branch spawns only the specialists needed for its scope, reconciles their results and returns one consolidated handoff. Reuse review agents for detailed design where practical.

Provide approved quality/security/recovery constraints before backend Architecture starts. Backend executes ordered sibling stages: Architecture → Identity/Access → Middleware → Diagnostics → conditional Delivery/Operations → final Quality Attributes review. Frontend also captures approved experience/quality constraints before its ordered sibling stages: conditional Experience UX baseline → Frontend Architecture → Components and State → Experience detail → Quality and Delivery. Both branches use dedicated specialist workflows with accepted predecessor decisions. Backend and frontend remain parallel branches; internal stage ordering does not make them a chain. Later data/policy/recovery requirements return to their original owners and reopen only affected downstream evidence.

If a named adapter is unavailable, use an available general-purpose subagent with the explicit branch workflow path and bounded assignment. Do not assume an adapter exists merely because its source file is in the library.

When this coordinator runs in the main chat, branches occupy the first child level and their specialists the next. Account for the actual available depth and shared concurrency budget; keep parents' occupied slots in that budget. Queue specialist work rather than assuming every branch can fill the session limit. At a leaf, request a sibling assignment from the parent instead of spawning further. If only shallow delegation is available, run branch profiles within their separate branch sessions; if delegation is unavailable, report the pending branch work without loading its skills into this coordinator.

### 5. Coordinate changes and consolidate

Branches return contract-change requests with affected operation/decision IDs, rationale, compatibility impact and dependent work. Only this coordinator updates the shared contract. Pause affected work, reconcile the request with both affected branches, validate and version the accepted change, then reopen only affected decisions, diagrams, mocks/fixtures, verification and readiness. Unaffected assignments may continue. Reject or revalidate handoffs built against an obsolete affected baseline.

Resolve backend/frontend disagreements through their branch owners. Give system-level topology, cross-boundary sequences and every feature diagram one owner. Do not silently overwrite an accepted decision or let branches establish conflicting contract authorities.

### 6. Assemble the final design

Enforce the mandatory diagram-first presentation on every returned section before assembly. Return prose-first or missing-view content to its branch owner; do not manufacture a diagram in the main coordinator or load an extra skill. Write each accepted decision once into the artifacts below. Consolidated handoffs are transient; do not create persistent specialist packets or duplicate decision/routing registers. Use the Index for versions, coverage, routing, readiness and the review verdict. Keep only material unresolved cross-document decisions in the optional `open-decisions.md` with ID, decision needed, impact, owner, status and target artifact.

### 7. Apply the final readiness gate

Assess these checks directly, recording `Pass`, `Gap` or `Needs decision`, with evidence and an owner for gaps:

- **Sources and coverage:** every applicable approved obligation and actual operation maps to a feature, technical realization and verification; omissions differ from approved exclusions. Source versions and remaining approvals are visible.
- **Contract consistency:** applicable contract review and validation evidence is present; both branches and their examples/diagrams use the accepted version; authorization, error, state, concurrency, retry and compatibility behavior agrees across boundaries.
- **Visual design:** every substantive technical section opens with its relevant diagram(s), followed by supporting notes/specifications; the Index opens with its authority/navigation view. Reject prose-first sections and diagram placeholders. System-level target architecture, main flow and runtime/deployment topology are present; brownfield current/problem views have evidence. Every feature has a target technical-flow diagram plus applicable state, data, middleware and frontend views. Diagrams have stable IDs, ownership, traceability, readable sources and reported syntax/render validation or limitations.
- **Backend completeness:** branch evidence covers architecture and dependency direction, domain/data ownership, physical models, proposed DDL, parameterized DML/query catalog, transactions/access paths, migration/recovery and middleware behavior where applicable. Required data and middleware readiness is resolved.
- **Frontend completeness:** branch evidence covers routes, components, state/data, full UI states, responsive/accessibility/localization, performance, client security, observability and build/delivery where applicable, without transferring authoritative server rules to clients.
- **Quality and operations:** branch evidence maps security/privacy, resilience, performance/capacity, recovery, configuration, observability, deployment and support decisions to requirements, owners and verification. Planned checks are distinguished from checks actually executed.
- **Authority and readiness:** document/schema/database authorities agree, shared rules are not duplicated, material blockers are resolved, required sign-offs are recorded and no unapproved scope or implementation is introduced.

Return technical gaps to the owning branch; do not load another skill to repair them yourself. Recheck affected evidence after corrections. Overall `SD-Ready` requires all applicable branch, integration, contract, data and middleware gates and required approvals. A conditional/provisional result or unresolved material gap must not be reported as implementation-ready.

Claim completion only after every workflow step has a recorded outcome and every applicable step is complete. A `Blocked` or `Pending` applicable step prevents an overall readiness claim. Report checks that have been planned but not run as pending verification; assess them against the evidence required for this design stage rather than claiming implementation tests have passed.

### 8. Report and hand off

Report the workflow outcomes and readiness evidence using the expected output below. Hand the accepted baseline to `spec-driven-development-agent` only after the applicable final gate passes; otherwise report blockers and the next owner action. Implementation remains a separately authorized lifecycle stage.

## Expected output

Include a brief numbered record of steps 1 through 8 with each status (`Complete`, `Not Applicable`, `Blocked` or `Pending`), outcome, evidence or next action, and reasons for any `Not Applicable` or `Blocked` steps. Record it in the SD Index when artifact edits are authorized; for review-only work, include it in the review response without changing the baseline. This record is required for focused tasks as well as full designs.

Return authoritative artifact paths, contract version/hash, source-to-feature coverage, applicable `Contract-Ready`, `Backend-Ready`, `Frontend-Ready`, `Integration-Ready`, `Data-Ready`, `Middleware-Ready` and overall `SD-Ready` results, blockers/owners and next action. Distinguish actual validation evidence from planned checks, and a review verdict from approval. If work stops early, report the available outcomes and pending dependent steps without claiming workflow completion.

## Assignment and return contract

Send each branch: mode; bounded scope and feature/operation IDs; source paths/versions/status; contract path/version/hash; accepted shared decisions; constraints/current evidence; unresolved inputs; expected diagrams/artifacts and verification; mandatory diagram-first section order and visual coverage; allowed delegation and write ownership. References to relevant sections are preferable to copied source histories.

Require diagram-first technical content under the presentation policy above, followed by supporting details and numbered workflow outcomes. Require one consolidated return with: source/contract baseline; feature and diagram coverage; accepted decisions with rationale, consequences and target sections; complete assigned design/diagram/database content; exact contract-change requests or `None`; dependencies and blockers; verification evidence versus planned checks; branch readiness recommendation. The main coordinator remains the final writer unless an exclusive bounded artifact write is explicitly assigned. Shared API contracts, Integration SD and overall readiness remain its responsibility.

## Artifact authorities

Use project conventions, otherwise:

| Artifact | Default path | Authority |
|---|---|---|
| SD Index | `output/SD/SD-<project>-index.md` | Sources, version/hash register, branch routing/status, feature/diagram coverage, readiness, review and approvals |
| Backend SD | `output/SD/SD-<project>-backend.md` | Backend internals, data semantics and server enforcement |
| Frontend SD | `output/SD/SD-<project>-frontend.md` | Client internals and behavior |
| Integration SD | `output/SD/SD-<project>-integration.md` | Cross-boundary semantics, identity exchange, failures, compatibility and verification |
| API contracts | `output/SD/contracts/openapi.yaml` or the existing contract layout | HTTP operation, field and protocol structure; retain other applicable schema formats |
| Database design | `output/SD/database/` | Affected physical schema, proposed DDL, DML/query catalog and related artifacts |
| Diagrams | `output/SD/diagrams/` | Maintained sources and available rendered views linked from their owning documents |
| Optional open decisions | `output/SD/work/<project>/open-decisions.md` | Unresolved material coordination only |

Create only applicable artifacts. Use stable feature, operation, diagram, decision and verification IDs. Approved requirements govern intended behavior; any disagreement among contract structure, integration semantics, database artifacts and branch internals blocks affected readiness until reconciled.

This is design work: do not write production code, execute migrations, deploy, mutate infrastructure, embed secrets or silently change requirements.
