---
name: prd-standard
description: Create or audit structured, AI-ready Product Requirements Documents with problem framing, target users, measurable outcomes, user stories, prioritized requirements, UX, scope, risks, milestones, and open decisions; use for product requirements, not standalone system architecture or code implementation.
---

# Standard PRD Authoring and Review

Use this skill when the user wants to create, refine, compare, or quality-check a Product Requirements Document (PRD), especially one that will guide both product teams and AI coding tools.

The PRD is the product source of truth: why the product exists, who it serves, what behavior is needed, how success is measured, and what is explicitly out of scope. It is not automatically an architecture document or an authorization to make technical choices.

## Core operating rules

- Treat user-provided facts, research, and confirmed decisions as the source of truth.
- Never invent personas, market numbers, willingness to pay, metrics, launch dates, budgets, stakeholder approvals, technology choices, or integrations.
- Label uncertainty explicitly as `Confirmed`, `Proposed`, `Assumption`, `TBC`, or `Pending Approval`.
- Keep product requirements separate from implementation proposals. Technical details supplied by the user may be preserved as proposed constraints, but must not be presented as approved architecture.
- Use plain, testable language. Avoid “fast”, “seamless”, “intuitive”, or “real-time” unless the document defines an observable threshold.
- Do not silently resolve conflicts. Capture them as open questions or decisions.
- Do not generate code, API contracts, database schemas, or system architecture unless the user separately asks for those deliverables.

## Diagram dependency

When a PRD needs a diagram, invoke/read `plantuml-syntax` before creating or modifying PlantUML. Use it conditionally for journeys, use cases, workflows, state behavior, scope hierarchies, timelines, WBS, or wireframes; keep the required product behavior and acceptance meaning in text.

## Input classification

### Mandatory inputs

- Task mode: draft, refine, compare, or review.
- Product or feature identity and requested release/scope when known.
- For a new PRD: the product problem/opportunity, target outcome, and known users or scope.
- For refinement or review: the complete PRD or document under review.

### Conditional inputs

- A BRD is mandatory when one exists or when the product work is governed by business requirements; if no BRD is required, record an explicit user waiver.
- Research, analytics baselines, UX references, legal/compliance constraints, technical constraints, integrations, and Change Requests are mandatory when the requested decision depends on them; otherwise record `Not Provided`, `TBC`, or `Not Applicable`.
- SRS and FRS are conditional downstream artifacts and are not required for a PRD-only request.

### Optional context

- Competitive examples, screenshots, wireframes, preferred wording, and supplementary references may improve the PRD but never constitute approval.

## Workflow

1. Classify the task as drafting, refining, or reviewing a PRD.
2. Extract the product context, problem evidence, target users, goals, success metrics, scope, constraints, dependencies, and unresolved decisions.
3. For a full draft or review, read [references/prd-template.md](references/prd-template.md) and adapt the sections to the product and release size.
4. Convert desired behavior into user stories, functional requirements, and acceptance criteria. Ensure the user story and requirement describe the same outcome.
5. Prioritize features consistently:
   - `P0`: required for the stated release to be usable or viable;
   - `P1`: important for a credible v1 but can follow P0;
   - `P2`: valuable enhancement or delighter that can wait.
6. Separate product status from priority:
   - Priority: `P0`, `P1`, `P2`.
   - Decision status: `Confirmed`, `Proposed`, `TBC`, `Pending Approval`.
   - Delivery status: `MVP`, `v1`, `v1.x`, or a named phase.
7. Run [references/quality-gate.md](references/quality-gate.md). For reviews, report structural completeness, requirement quality, decision readiness, and implementation-boundary issues separately.
8. End with open questions that have enough context for a product owner or stakeholder to decide.

## Recommended PRD structure

Use the 13-section AI-ready structure as the baseline:

1. Overview
2. Problem Statement
3. Target Users
4. Goals and Success Metrics
5. User Stories
6. Functional Requirements
7. Non-Functional Requirements
8. Technical Considerations
9. UI/UX Requirements
10. Out of Scope
11. Timeline and Milestones
12. Risks and Mitigations
13. Open Questions

Add document control, assumptions and constraints, dependencies, release acceptance criteria, version history, and approval/sign-off when the project needs them. Omit irrelevant sections rather than filling them with generic text, but do not omit a section merely because its information is currently unknown; mark it `TBD` when it affects a delivery decision.

## Requirement writing standard

For full authoring/review, or a BRD-to-PRD coverage gap, use [functional coverage](references/functional-coverage.md). Expand umbrella capabilities into testable actor operations and reconcile every upstream item in scope. Reuse the PRD or its approved companion for the detailed catalogue.

Use stable IDs and observable outcomes. For example:

> `US-01` — As a customer, I want to choose a delivery date so that I can receive the product when needed.
>
> `FR-DEL-001` — The product must show only delivery dates that satisfy the configured lead-time and availability rules.

For each important requirement, make clear:

- actor or target user;
- entry surface or trigger, stable source ID, delivery phase and explicit disposition;
- desired behavior and user/business benefit;
- entry conditions and relevant exceptions;
- priority and decision status;
- acceptance criteria;
- analytics or success signal when applicable.

Acceptance criteria should cover the happy path, validation, permissions, empty states, failure behavior, and boundary conditions where relevant. Use Given/When/Then or a concise expected-result table when it improves testability.

## Technical considerations boundary

The article's technical section is useful for AI-assisted implementation, but it must be handled carefully:

- Keep product-level constraints, required integrations, data sensitivity, compatibility targets, and approved platform restrictions in the PRD.
- Put API endpoint shapes, database schemas, file layouts, framework choices, class design, and detailed algorithms in SA/SRS or an implementation plan.
- If the user supplies technical choices, preserve them in a clearly labeled `Proposed` or `Confirmed constraint` subsection rather than silently treating them as design approval.
- Never include secrets, tokens, credentials, or private production configuration.

## Deliverable conventions

- Use Markdown headings and tables for scannability.
- Keep section numbering stable when refining an existing PRD.
- Keep a feature-to-user-story-to-acceptance-criteria relationship for critical paths.
- Distinguish product outcome metrics from delivery milestones and engineering health metrics.
- When creating a file and no destination is supplied, use `output/PRD/PRD-<project-name>.md` or the user's existing project convention.
- Do not claim the PRD is approved, ready for development, or complete while material decisions or sign-offs remain pending.
