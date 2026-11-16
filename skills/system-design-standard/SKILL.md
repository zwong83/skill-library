---
name: system-design-standard
description: Create or audit a visual-first, implementation-ready System Design set with system-level and per-feature technical diagrams, explicit data models, DDL/DML design, middleware topology/behavior, and separate backend, frontend, integration, index, and machine-readable authorities.
---

# Standard System Design

Turn an approved System Analysis and requirements baseline into an explicit, reviewable technical design. Keep authoritative backend, frontend, and integration concerns separate so each participant loads only the context it needs.

## Relationship to the agent workflow

The main `system-design-agent` does not invoke this skill. Its coordination workflow, API ownership and final readiness gate live directly in [its SKILL.md](../../agents/system-design-agent/SKILL.md), and its only additional skill is `api-design-standard`.

When a backend/frontend branch or leaf invokes this skill, apply only its assigned technical artifact, diagram, data/middleware and quality-gate sections. Do not run the standalone orchestration workflow below, spawn another branch coordinator, redefine the main coordinator's API ownership or claim overall readiness. The workflow below is for standalone System Design authoring/review outside those delegated assignments.

## Core rules

- Treat approved requirements, System Analysis, confirmed constraints, and explicit decisions as the source of truth.
- Never invent scope, approval, security/compliance policy, capacity targets, vendors, ownership, or operational commitments.
- Label uncertainty as Confirmed, Proposed, Assumption, TBC, Pending Approval, Open, or Deferred.
- Prefer the simplest design that satisfies behavior and quality requirements.
- State material decisions with driver, rationale, consequences, owner, and status.
- Treat security, privacy, reliability, performance, operability, recovery, cost, and verification as first-class concerns.
- Do not write production code or execute deployment, migration, infrastructure, or external changes.

## Inputs and readiness

Mandatory:

- task mode and system/feature scope;
- complete approved System Analysis for new design work, unless a provisional design is explicitly requested;
- complete existing applicable SD set for refinement/review.

BRD/PRD/SRS/FRS, Change Request, UX/user flows/wireframes/design system, browser/device/locale/accessibility, security/privacy, performance, availability, recovery, observability, deployment, operations, integration, migration, compatibility, vendor, platform, and capacity inputs become mandatory only when a decision depends on them.

Read the governing source documents completely. For brownfield work, use verified current-system evidence. Mark missing evidence as unknown and block readiness that depends on it. Label an explicitly requested provisional design as provisional. Block `SD-Ready` when a material decision, requirement, or approval is unresolved.

## Visual-first and per-feature diagram policy

Use diagrams as the primary explanation for the overall system and every in-scope feature. A full SD must show current logic/problems for brownfield scope, target architecture and main runtime flow, deployment/middleware topology, logical/physical data models when data is material, and a dedicated target technical-flow diagram for every feature.

For standalone design or unrestricted diagram authors, invoke `plantuml-syntax` before creating or changing PlantUML and load only the relevant syntax reference. A specialist with an explicit skill allowlist instead uses existing diagram conventions/templates and installed syntax/render tooling within its assignment; do not bypass that allowlist through this reference. Required views and validation evidence still apply. Keep prose short; use compact tables and normative text only for exact contracts, rules, parameters, constraints, exceptions, targets, decisions, procedures, traceability and unresolved items. Every diagram needs an ID, title, scope, As-Is/To-Be status, meaning, assumptions/legend, owner and source/feature/decision traceability. Resolve diagram/text conflicts before readiness.

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

**For standalone System Design authoring/review, follow steps 1 through 8 in order.** Delegated branches use only their assigned technical sections as described above. Record each applicable outcome, including a reason for any `Not Applicable` step. Existing decisions and evidence can satisfy an applicable step when confirmed. Mark missing material inputs or decisions `Blocked` and stop work that depends on them. Record step outcomes briefly in the Index or review findings.

1. **Establish the baseline.** Confirm the task mode, scope, source versions and approvals, constraints, decision criteria, and current-system evidence using the input rules above.
2. **Reconcile coverage and select routes.** Check the complete approved BRD functional inventory or authorized equivalent against the PRD and SA, using the [shared functional coverage method](../prd-standard/references/functional-coverage.md) when applicable. Record upstream gaps and approved dispositions. In the Index, record feature/diagram coverage, one owner per required view, and selected routes with the reason and source IDs. Use [specialist routing](references/specialist-routing.md) and load only the activated profiles.
3. **Establish architecture and shared contracts.** Define or confirm the affected context, components, ownership, runtime flow and topology from the baseline. Use `api-design-standard` for shared HTTP/OpenAPI design. In agent-coordinated work, the main coordinator authors the contract and backend/frontend branches review it; apply the [contract-first handoff](../../agents/system-design-agent/references/specialist-coordination.md#backend-first-contract-then-parallel-detail). Preserve accepted versions and reconcile applicable feedback before `Contract-Ready`.
4. **Develop or verify the affected design.** Ensure each in-scope feature has a target technical flow and applicable component, state, data, middleware, failure/recovery, or frontend views. Include current/problem evidence for brownfield scope. For durable data or middleware, produce or verify the applicable physical model, proposed DDL, parameterized DML/query catalog, transactions, access paths, migrations/recovery, middleware topology and interactions, controls, and verification. Reconcile runtime topology and ownership where affected. Backend and frontend detail may proceed in parallel once their shared contract is ready.
5. **Reconcile handoffs and assemble the design.** Enforce diagram-first section order and reject missing-view or prose-first technical handoffs before assembly. Record accepted decisions once in the authoritative artifacts. Keep only material unresolved cross-document decisions in the optional `open-decisions.md` file. For reviews, report findings against the existing artifacts.
6. **Confirm traceability.** Link each applicable obligation from requirements and SA through feature diagrams, technical decisions and artifacts, and verification evidence or planned checks.
7. **Apply the quality gate.** Use the relevant [quality gate sections](references/quality-gate.md). Check the full applicable design when claiming overall readiness. Resolve gaps through their owners and rerun affected checks. Record the verdict and remaining gaps in the Index.
8. **Report readiness.** Record the applicable contract, data, middleware, Backend/Frontend/Integration, and overall SD statuses. Distinguish review results and planned verification from actual approval. A scoped review reports only the readiness it verified.

## Reference routing

Start with the current step. Open another file or section only to answer a requirement, dependency, or finding. In delegated work, the selected specialist loads its own technical skill and the relevant section. Apply the same profiles sequentially when delegation is unavailable or unauthorized.

| Need | Open |
|---|---|
| Decide which specialist owns an affected concern | [Specialist routing](references/specialist-routing.md) |
| Assign or reconcile specialist work | [Coordination contract](../../agents/system-design-agent/references/specialist-coordination.md), limited to the applicable handoff or coordination section |
| Create or update the Index | [Index template](references/sd-index-template.md), using the relevant sections |
| Select document authorities or resolve a conflict | [Document-set rules](references/system-design-template.md), when the existing assignment does not settle it |
| Create or check design content | Only the affected [Backend](references/backend-sd-template.md), [Frontend](references/frontend-sd-template.md), or [Integration](references/integration-sd-template.md) template or section |
| Define or verify a diagram or its coverage | Applicable [feature diagram coverage](references/feature-diagram-coverage.md). Use the full reference for full design or readiness coverage. |
| Design or verify data or middleware artifacts | The data, query, or middleware section of [data and middleware artifacts](references/data-and-middleware-artifacts.md) |
| Check the design | [Quality gate](references/quality-gate.md), scoped to the requested verdict |

## Authority and artifact boundaries

- Machine-readable contracts own field/protocol structure.
- Versioned database artifacts own affected physical schema/DDL and the critical DML/query catalog; Backend SD owns their semantics, transactions, migration, and recovery.
- Integration SD owns cross-boundary behavior and contract evolution.
- Backend SD owns backend internals and server-side enforcement.
- Frontend SD owns frontend internals and client behavior.
- Index owns source/artifact versions, routing/status, readiness, unresolved items, review verdict, and approvals.

Do not duplicate a full schema or the same normative rule across documents. Cross-reference the authority. Any disagreement blocks readiness until reconciled.

Use stable IDs such as DES-ARCH-001, FEAT-001, DIA-FEAT-001, CMP-001, API-001, DATA-001, DDL-001, DML-001, MW-001, SEQ-001, SEC-001, NFR-001, ADR-001, and TEST-001.

When no destination is specified, use:

- `output/SD/SD-<project-name>-index.md`
- `output/SD/SD-<project-name>-backend.md` when applicable
- `output/SD/SD-<project-name>-frontend.md` when applicable
- `output/SD/SD-<project-name>-integration.md` when applicable
- `output/SD/diagrams/` for maintained PlantUML sources and optional rendered previews linked by diagram ID
- `output/SD/contracts/` for applicable machine-readable contracts
- `output/SD/database/` for applicable physical model, proposed DDL/DML, access-path, transaction/concurrency, and migration design artifacts

Keep production code, live mutations, migration execution, secrets, private production configuration, and unapproved vendor commitments out. Never call the set approved or implementation-ready while material decisions, controls, ownership, evidence, or sign-offs remain pending.
