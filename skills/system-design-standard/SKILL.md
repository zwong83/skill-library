---
name: system-design-standard
description: Create or audit implementation-ready System Design documents covering architecture, component responsibilities, interfaces, data design, sequences, security, reliability, observability, deployment, trade-offs, and verification without writing production code.
---

# Standard System Design

Use this skill to turn an approved System Analysis and requirements baseline into an explicit, reviewable technical design. It is the governing standard; specialized skills are lazy-loaded only when the routing decision says their concern is material.

## Core rules

- Treat approved requirements, System Analysis, confirmed constraints, and explicit decisions as the source of truth.
- Never invent scope, approval, security/compliance policy, capacity targets, vendors, ownership, or operational commitments.
- Label uncertainty as Confirmed, Proposed, Assumption, TBC, Pending Approval, Open, or Deferred.
- State each material decision, driver, alternatives, rationale, trade-offs, consequences, owner, and status.
- Prefer the simplest design that satisfies behavior and quality requirements.
- Treat security, privacy, reliability, performance, operability, recovery, cost, and verification as first-class concerns.
- Do not write production code or execute deployment, migration, infrastructure, or external changes.

## Progressive skill routing

Before loading a companion skill, read [references/specialist-routing.md](references/specialist-routing.md) and classify each concern as Required, Conditional, or Not Applicable with evidence. Load only Required concerns and Conditional concerns activated by the actual design.

In an agent-capable runtime, route bounded work to the matching specialist Agent and merge its decision packet. In a single-agent runtime, apply the same profiles sequentially. Do not load every specialized skill merely because it appears in the template.

## Inputs and readiness

Mandatory:

- task mode and system/feature scope;
- complete approved System Analysis for new design work, unless a provisional design is explicitly requested;
- complete existing SD for refinement/review.

BRD/PRD/SRS/FRS, Change Request, UX/user flows/wireframes/design system, browser/device/locale/accessibility, security/privacy, performance, availability, recovery, observability, deployment, operations, integration, migration, compatibility, vendor, platform, and capacity inputs become mandatory only when a decision depends on them.

Read identified sources completely. Block an implementation-ready conclusion when material behavior, ownership, interface, data, security, performance, reliability, deployment, operational, acceptance, or approval decisions remain unresolved.

## Diagram policy

Use focused diagrams when they materially clarify boundaries, relationships, flows, state, timing, deployment, or ownership. Invoke plantuml-syntax only before creating or changing PlantUML and load only the relevant diagram reference. Use object-oriented-design or design-patterns only when the selected paradigm or a real pattern decision requires them.

Text remains normative for contracts, rules, constraints, exceptions, targets, decisions, and procedures. Every diagram needs a title, scope, meaning, assumptions/legend, and source traceability. Resolve diagram/text conflicts before readiness.

## Workflow

1. Read [references/system-design-template.md](references/system-design-template.md) for a full draft or structural review.
2. Establish source baseline, architecture drivers, constraints, quality attributes, scope, and decision criteria.
3. Build the specialist routing matrix and provide each selected concern only the relevant sources.
4. Define context, components, responsibilities, boundaries, flows, ownership, and approved topology.
5. Incorporate selected specialist decisions for interfaces/data, frontend, quality attributes, and delivery/operations.
6. For frontend scope, establish backend authority and a draft contract, reconcile frontend contract feedback, record `Contract-Ready`, then allow backend/frontend detail to proceed in parallel from the versioned contract.
7. Reconcile cross-concern dependencies and conflicts; do not silently choose between unresolved material proposals.
8. Record alternatives, risks, assumptions, dependencies, open decisions, implementation prerequisites, and approval status.
9. Maintain: Analysis requirement/flow -> design decision/component/interface/data model -> verification evidence.
10. Run [references/quality-gate.md](references/quality-gate.md) and resolve blocker/major gaps through the owning source or specialty.
11. End with readiness status and the next authorized action.

## Artifact boundaries

The SD may contain architecture, components, layers/modules, interfaces, data, sequences/states, frontend rendering/routing/components/state/data/experience, security, resilience, performance/capacity, configuration, deployment/release, observability/operability, verification, ADRs, risks, and trade-offs.

Keep production code, live mutations, migration execution, secrets, private production configuration, and unapproved vendor commitments out unless separately requested and authorized.

Use stable IDs such as DES-ARCH-001, CMP-001, API-001, DATA-001, SEQ-001, SEC-001, NFR-001, ADR-001, and TEST-001. Preserve section numbering during refinement.

When no destination is specified, use output/SD/SD-<project-name>.md. Never call the design approved or implementation-ready while material decisions, controls, ownership, evidence, or sign-offs remain pending.
