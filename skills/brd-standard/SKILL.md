---
name: brd-standard
description: Create or audit decision-ready Business Requirements Documents using a structured, business-first format with scope, measurable objectives, numbered requirements, business rules, data, risks, UAT, open decisions, and approval control; use for BRD work, not technical architecture or implementation specifications.
---

# Standard BRD Authoring and Review

Use this skill when the user wants to create, refine, compare, or quality-check a Business Requirements Document (BRD). The output must help business stakeholders agree on the problem, desired outcomes, scope, rules, priorities, and approval status before solution design begins.

## Core operating rules

- Treat user-provided facts and confirmed stakeholder decisions as the source of truth.
- Never invent owners, targets, budgets, dates, policies, legal conclusions, approval status, or technical interfaces.
- Mark uncertainty explicitly as `Proposed`, `Assumption`, `TBC`, `Open`, or `Pending Approval`.
- Preserve the difference between a business requirement and a proposed solution. A suggestion is not a confirmed rule.
- Use plain business language. Keep implementation details only when they express a business constraint or acceptance condition.
- Do not silently resolve contradictions. Call them out and place them in `Open Business Decisions`.
- Do not produce architecture, API contracts, database schemas, or implementation tasks unless the user separately requests those deliverables.

## Workflow

1. Identify whether the task is drafting, refining, or reviewing a BRD.
2. Extract confirmed facts, stakeholder roles, scope boundaries, measurable outcomes, unresolved decisions, and source terminology.
3. For drafting or a full review, read [references/brd-template.md](references/brd-template.md) and adapt its modules to the domain. Do not force irrelevant sections.
4. Write or assess requirements as stable, testable statements with a unique identifier, priority, and acceptance criteria where useful.
5. Separate three kinds of status:
   - **Priority**: `Must`, `Should`, `Could`, `Won't for this phase`.
   - **Decision status**: `Confirmed`, `Proposed`, `TBC`, `Pending Approval`.
   - **Delivery status**: `MVP`, `Later`, or a named release phase.
6. Normalize terminology and flag mixed labels such as `Proposed Must` unless the document defines them.
7. Run the checks in [references/quality-gate.md](references/quality-gate.md). For a review, report both what is structurally correct and what remains unconfirmed or weak.
8. End with the smallest useful set of open decisions, owners/approvers when known, and the next approval step.

## Requirement writing standard

Prefer statements such as:

> `BR-ORD-001` — The system must create one unique order record for each accepted checkout request.

Each requirement should make clear, where applicable:

- who needs the capability;
- what business outcome or rule is required;
- when the rule applies;
- priority and decision status;
- observable acceptance criteria;
- dependencies or exceptions.

Avoid vague wording such as “easy”, “fast”, “seamless”, or “real-time” without a measurable definition. Keep historical snapshots, audit trails, idempotency, concurrency, privacy, and recovery requirements when they protect a stated business outcome; move their implementation mechanics to SA/SRS.

## Review verdicts

When reviewing an existing BRD, distinguish these conclusions:

- **Format completeness**: whether the expected BRD sections are present.
- **Requirement quality**: whether requirements are clear, atomic, prioritized, and testable.
- **Decision readiness**: whether unresolved policies are visible and assigned for approval.
- **Delivery readiness**: whether scope, UAT, release gates, risks, and dependencies are sufficiently defined.

Do not call a BRD “approved” or “ready for development” when its own approval table or key business decisions are still pending.

## Deliverable conventions

- Use Markdown headings and tables when they improve comparison.
- Keep section numbering stable when refining an existing BRD.
- Preserve the original language and domain terms unless the user asks for translation or normalization.
- When creating a file and no destination is supplied, use a project-specific folder such as `output/BRD/<project-name>/BRD-<project-name>.md`; do not reorganize unrelated files.
- If the user asks only whether a BRD format is correct, review it first and do not rewrite it unless requested.
