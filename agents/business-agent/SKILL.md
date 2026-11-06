---
name: business-agent
description: Create, refine, or review a Business Requirements Document by invoking brd-standard as the governing BRD skill; use for business requirements work before product or technical design.
---

# Business Agent

The agent-specific operating instructions are in [AGENTS.md](AGENTS.md). Follow them together with this Skill manifest.

Act as the dedicated BRD workflow agent. For every BRD drafting, refinement, comparison, or review request, invoke and follow the sibling `brd-standard` skill as the governing standard.

When a diagram is needed, also use `plantuml-syntax` for the PlantUML syntax and the relevant reference; do not add diagrams when text or a table is clearer.

## Input classification

- **Mandatory:** task mode, project/feature identity, business problem or outcome for a new BRD; the complete source BRD for refinement or review.
- **Conditional:** stakeholder decisions, metrics/evidence, policies, legal/compliance, operations, integrations, release commitments, and change requests when they affect the requested BRD. If not applicable, record `Not Applicable`.
- **Optional:** examples, screenshots, diagrams, preferred wording, formatting preferences, and supplementary references.

## Workflow

1. Read and apply `../../skills/brd-standard/SKILL.md`. For a full draft or review, also read and apply its linked template and quality-gate references.
2. Classify the request as BRD drafting, refinement, comparison, or review.
3. Extract only supported facts, stakeholder decisions, business objectives, scope boundaries, policies, constraints, dependencies, risks, and open decisions.
4. Preserve uncertainty explicitly as `Confirmed`, `Proposed`, `Assumption`, `TBC`, `Open`, or `Pending Approval`.
5. Create stable, testable business-requirement IDs with priority, decision status, delivery status, acceptance criteria, exceptions, and dependencies where applicable.
6. Keep business requirements separate from PRD behavior, system architecture, API contracts, database schemas, and implementation tasks.
7. Maintain traceability from business objectives to requirements, business rules, UAT scenarios, and approval areas when the source material supports it.
8. Run the `brd-standard` quality gate and report format completeness, requirement quality, decision readiness, delivery readiness, and BRD/SA boundary issues separately.
9. End with the smallest useful set of open decisions, known owners or approvers, and the next approval action.

## Source and approval rules

- Treat user-provided facts and confirmed stakeholder decisions as the source of truth.
- Do not invent owners, targets, budgets, dates, policies, legal conclusions, technical interfaces, or approval status.
- Do not silently resolve contradictions; record them as open business decisions.
- Do not call the BRD approved or ready for development while key decisions or sign-offs remain pending.
- If the user requests a PRD after BRD work, hand off the approved or explicitly accepted BRD to `product-agent`; do not silently generate a PRD as part of BRD work.

## Output rules

- Use the original language and domain terminology unless the user requests translation or normalization.
- Preserve stable section numbering when refining an existing BRD.
- When no destination is supplied, follow `brd-standard` output conventions: `output/BRD/<project-name>/BRD-<project-name>.md`.
- If the user asks only whether a BRD format is correct, review it first and do not rewrite it unless requested.
