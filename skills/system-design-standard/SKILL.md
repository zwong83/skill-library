---
name: system-design-standard
description: Create or audit an implementation-ready System Design set with separate backend, frontend, integration, index, and machine-readable contract authorities without duplicating specialist process notes.
---

# Standard System Design

Turn an approved System Analysis and requirements baseline into an explicit, reviewable technical design. Keep authoritative backend, frontend, and integration concerns separate so each participant loads only the context it needs.

## Core rules

- Treat approved requirements, System Analysis, confirmed constraints, and explicit decisions as the source of truth.
- Never invent scope, approval, security/compliance policy, capacity targets, vendors, ownership, or operational commitments.
- Label uncertainty as Confirmed, Proposed, Assumption, TBC, Pending Approval, Open, or Deferred.
- Prefer the simplest design that satisfies behavior and quality requirements.
- State material decisions and preserve alternatives/trade-offs only when their rationale must survive review.
- Treat security, privacy, reliability, performance, operability, recovery, cost, and verification as first-class concerns.
- Do not write production code or execute deployment, migration, infrastructure, or external changes.

## Progressive routing and context control

Read [references/specialist-routing.md](references/specialist-routing.md), classify each concern as Required, Conditional, or Not Applicable with evidence, and load only the activated specialists/skills.

In an agent-capable runtime, specialists return the compact handoff defined by `system-design-agent`; the Coordinator writes accepted content once into the authoritative target. In a single-agent runtime, apply the same profiles sequentially without producing intermediate packet files.

Read [references/system-design-template.md](references/system-design-template.md) first. Then load only the document templates required by scope:

- [references/sd-index-template.md](references/sd-index-template.md) for every SD set;
- [references/backend-sd-template.md](references/backend-sd-template.md) when backend/service/data/runtime scope exists;
- [references/frontend-sd-template.md](references/frontend-sd-template.md) when a frontend application is in scope;
- [references/integration-sd-template.md](references/integration-sd-template.md) when a frontend/backend, service/service, event, external-system, or other cross-boundary contract exists.

Do not load all templates merely because they exist.

## Inputs and readiness

Mandatory:

- task mode and system/feature scope;
- complete approved System Analysis for new design work, unless a provisional design is explicitly requested;
- complete existing applicable SD set for refinement/review.

BRD/PRD/SRS/FRS, Change Request, UX/user flows/wireframes/design system, browser/device/locale/accessibility, security/privacy, performance, availability, recovery, observability, deployment, operations, integration, migration, compatibility, vendor, platform, and capacity inputs become mandatory only when a decision depends on them.

Read identified sources completely. Block `SD-Ready` when material behavior, ownership, interface, data, security, performance, reliability, deployment, operational, acceptance, or approval decisions remain unresolved.

## Diagram policy

Use focused diagrams when they materially clarify boundaries, relationships, flows, state, timing, deployment, or ownership. Invoke `plantuml-syntax` only before creating or changing PlantUML and load only the relevant diagram reference.

Text remains normative for contracts, rules, constraints, exceptions, targets, decisions, and procedures. Every diagram needs a title, scope, meaning, assumptions/legend, and source traceability. Resolve diagram/text conflicts before readiness.

## Workflow

1. Establish source baseline, architecture drivers, constraints, quality attributes, scope, and decision criteria.
2. Build the specialist routing/status table in the Index and provide each selected concern only relevant context.
3. Define context, components, responsibilities, boundaries, flows, ownership, and approved topology in the applicable authoritative document.
4. For frontend scope, establish backend authority and a versioned draft contract, reconcile frontend feedback, record `Contract-Ready`, then allow backend/frontend detail to proceed in parallel.
5. Reconcile compact handoffs and write accepted results directly to Backend, Frontend, Integration, or Index; do not retain duplicate packet documents.
6. Keep only material unresolved cross-document decisions in the optional `open-decisions.md` working file.
7. Maintain `Analysis requirement/flow -> design decision/component/interface/data model -> verification evidence`.
8. Run [references/quality-gate.md](references/quality-gate.md), resolve blocker/major gaps through the owning source or specialty, and record the review verdict in the Index.
9. End with Backend/Frontend/Integration readiness and overall `SD-Ready`; do not fabricate approval.

## Authority and artifact boundaries

- Machine-readable contracts own field/protocol structure.
- Integration SD owns cross-boundary behavior and contract evolution.
- Backend SD owns backend internals and server-side enforcement.
- Frontend SD owns frontend internals and client behavior.
- Index owns source/artifact versions, routing/status, readiness, unresolved items, review verdict, and approvals.

Do not duplicate a full schema or the same normative rule across documents. Cross-reference the authority. Any disagreement blocks readiness until reconciled.

Use stable IDs such as DES-ARCH-001, CMP-001, API-001, DATA-001, SEQ-001, SEC-001, NFR-001, ADR-001, and TEST-001.

When no destination is specified, use:

- `output/SD/SD-<project-name>-index.md`
- `output/SD/SD-<project-name>-backend.md` when applicable
- `output/SD/SD-<project-name>-frontend.md` when applicable
- `output/SD/SD-<project-name>-integration.md` when applicable
- `output/SD/contracts/` for applicable machine-readable contracts

Keep production code, live mutations, migration execution, secrets, private production configuration, and unapproved vendor commitments out. Never call the set approved or implementation-ready while material decisions, controls, ownership, evidence, or sign-offs remain pending.
