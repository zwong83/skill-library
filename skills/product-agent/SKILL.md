---
name: product-agent
description: Orchestrate product-lifecycle requirements from BRD to PRD, SRS, and FRS using prd-standard, srs-standard, and frs-standard, with mandatory BRD intake and resolution gates.
---

# Product Agent

The agent-specific operating instructions are in [AGENTS.md](AGENTS.md). Follow them together with this Skill manifest.

Create, refine, or review product-lifecycle requirements only after completing both the BRD intake gate and the BRD resolution gate below. After both gates pass, use the sibling `prd-standard`, `srs-standard`, and `frs-standard` skills for the relevant lifecycle stages.

## Input classification

- **Mandatory:** task mode, product/feature identity, a complete BRD or explicit user waiver, and the complete PRD for refinement/review.
- **Conditional:** research, analytics baselines, UX references, legal/compliance constraints, technical constraints, SRS/FRS inputs, and Change Requests when the requested stage depends on them. If not applicable, record `Not Applicable`; if applicable but missing, block or mark the limitation explicitly.
- **Optional:** competitive examples, screenshots, wireframes, preferred wording, and supplementary references.

## Mandatory BRD intake gate

Before analyzing or drafting the PRD:

1. Check whether the user has supplied or explicitly identified a BRD through pasted content, an attachment, a local file path, a URL, or a named workspace document.
2. If a BRD is identified, obtain and read the relevant document completely before beginning PRD work. Record its title, version or date when available, approval status, and source location.
3. If no BRD is available, stop PRD work and ask the user to do one of the following:
   - provide or identify the BRD; or
   - explicitly confirm that this PRD may proceed without a BRD.
4. Do not treat silence, an unrelated document, a product idea, or an incomplete reference as confirmation that a BRD is unnecessary.
5. If multiple BRDs conflict and no authoritative version is clear, ask the user which one governs before proceeding.

The gate passes only when either:

- a BRD has been obtained and read; or
- the user has explicitly waived the BRD requirement for the current PRD task.

## Mandatory BRD resolution gate

If a BRD has been obtained, inspect it for unresolved business inputs before starting any PRD analysis or drafting. The gate must block when the BRD contains any unresolved item that can affect product scope, behavior, policy, priority, release, acceptance, or approval, including:

- `Assumption` items that have not been validated;
- `TBC`, `TBD`, `Open`, or equivalent undecided statuses;
- `Open Questions` or an open decision register with unanswered items;
- `Pending Approval`, missing sign-off, or unnamed decision ownership;
- unresolved conflicts, contradictions, or ambiguous rules;
- `Proposed` requirements, rules, constraints, or decisions that have not been explicitly accepted by the responsible business owner; and
- unresolved dependencies, risks, or exceptions that materially affect the PRD.

Do not silently convert any of these items into PRD assumptions or implementation choices. Before invoking `prd-standard`, produce a concise blocking register containing, for each item:

- source section and stable ID when available;
- unresolved statement;
- why it affects the PRD;
- decision or information required; and
- proposed decision owner when known.

Then ask the user to resolve or explicitly approve each blocking item. Stop the PRD workflow until the user provides the decisions, an updated BRD, or an explicit confirmation that a specific item is intentionally deferred and may be carried into the PRD as a clearly labeled `TBC`/`Pending Approval` item. A generic instruction such as “continue anyway” is not sufficient to bypass this gate.

The resolution gate passes only when all material unresolved items are resolved, explicitly approved, or individually deferred by the user with a clear acknowledgement of the resulting PRD limitation.

## BRD waiver handling

When the user explicitly confirms that no BRD is required:

- record `BRD Waiver: Confirmed by user` in Document Control or Source Evidence;
- state that business objectives, scope, policies, and constraints lack BRD validation;
- label unsupported inputs as `Assumption`, `TBC`, or `Pending Approval`;
- do not invent business approval or imply that the waiver makes the PRD approved; and
- include obtaining or validating the missing business requirements as a risk or open decision when material.

The no-BRD waiver bypasses BRD intake only; it does not silently approve unresolved product decisions. The PRD must still follow `prd-standard` decision-status rules and must surface its own assumptions, TBC items, pending approvals, and open questions.

## PRD workflow after the gate

1. Read and apply `../prd-standard/SKILL.md`. For a full draft or review, also follow the template and quality-gate references required by that skill.
2. Classify the request as PRD drafting, refinement, or review.
3. Extract from the BRD:
   - business problem and evidence;
   - objectives and measurable business outcomes;
   - stakeholders and target users;
   - confirmed scope and exclusions;
   - business rules, assumptions, constraints, dependencies, risks, and open decisions;
   - approval status and release expectations.
4. Preserve BRD decision status. Do not convert `Proposed`, `TBC`, `Pending Approval`, assumptions, or open decisions into confirmed product requirements.
5. Translate business needs into product goals, user journeys, user stories, functional and non-functional requirements, UX behavior, acceptance criteria, priorities, and release boundaries under `prd-standard`.
6. Maintain traceability for critical paths:

   `BRD objective or requirement -> PRD goal -> User story -> Functional requirement -> Acceptance criteria -> Metric`

7. Identify any PRD proposal that is not supported by the BRD as a product proposal or open decision, not as a confirmed requirement.
8. Run the `prd-standard` quality gate before delivery.

## Downstream SRS and FRS workflow

When the user requests a full product-lifecycle output or downstream specifications:

1. Read and apply `../srs-standard/SKILL.md`, including its template and quality gate.
2. Create or refine the SRS from the accepted or explicitly draft PRD, retaining BRD traceability and clearly labeling unresolved system decisions.
3. Read and apply `../frs-standard/SKILL.md`, including its template and quality gate.
4. Create or refine the FRS from the SRS as the primary source, with PRD/BRD traceability for product intent and business rules.
5. Do not silently resolve unresolved PRD/SRS decisions or claim implementation readiness while material behavior, interfaces, NFRs, permissions, acceptance criteria, dependencies, or approvals remain pending.

If the user requests PRD only, do not create SRS or FRS unless the user separately asks for the downstream stages.

## Document output strategy

Produce separate files by default:

- `output/PRD/PRD-<project-name>.md`
- `output/SRS/SRS-<project-name>.md`
- `output/FRS/FRS-<project-name>.md`

Keep each document focused on its lifecycle responsibility and connect them with a traceability matrix or lifecycle index when useful. Combine them only when the user explicitly requests a single-file deliverable.

## Output requirements

- Include a `Source BRD and Traceability` subsection that names the BRD or records the waiver.
- Surface BRD conflicts, missing approvals, and unresolved business decisions prominently.
- Do not begin substantive PRD drafting while the BRD resolution gate is blocked.
- Keep product requirements separate from architecture, API contracts, physical schemas, and code implementation.
- Use the output path and document conventions defined by `prd-standard` unless the user specifies another destination.
- Do not claim the PRD is approved or ready for development while material BRD or PRD decisions remain unresolved.

## First response when the BRD is missing

Ask one concise question and do not draft the PRD yet:

> Please provide or identify the BRD for this PRD. If no BRD is needed, explicitly confirm that I may proceed without one.
