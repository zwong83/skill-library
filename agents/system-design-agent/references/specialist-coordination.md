# System Design Specialist Coordination

The authoritative workflow is in [system-design-agent/SKILL.md](../SKILL.md). This reference preserves existing specialist entrypoints; it does not add a second coordination workflow or require the main coordinator to load another skill.

## Minimal context envelope

Use the [assignment and return contract](../SKILL.md#assignment-and-return-contract). A leaf receives a bounded assignment from its backend/frontend branch and returns to that branch. The branch consolidates results before returning to the main coordinator.

## Compact handoff contract

All branches and specialists follow the main coordinator's [mandatory diagram-first presentation](../SKILL.md#mandatory-diagram-first-presentation): diagrams lead each technical section; concise specifications and evidence follow, then workflow outcomes. Reject missing-view or text-first technical handoffs before consolidation. This adds no skill invocation or artifact authority.


Return source/contract versions, assigned feature/diagram coverage, accepted decisions and complete assigned content, exact contract-change requests or `None`, dependencies/blockers, and verification evidence versus planned checks. Use the [authoritative return requirements](../SKILL.md#assignment-and-return-contract); do not retain raw transcripts or persistent specialist packets.

## Runtime delegation rules

The main coordinator delegates to [backend-design-agent](../../backend-design-agent/SKILL.md) and [frontend-design-agent](../../frontend-design-agent/SKILL.md). Backend runs ordered sibling stages: Architecture, Identity/Access, Middleware, Diagnostics, conditional Delivery/Operations, then final Quality Attributes review. Frontend runs ordered sibling stages: conditional Experience UX baseline → Frontend Architecture → Components and State → Experience detail → Quality and Delivery. Both branches capture applicable constraints before architecture and consolidate their dedicated agents under their own mandatory workflows. Pass accepted predecessor decisions forward within the actual runtime depth and shared concurrency budget. Leaves request additional specialists through their parent; later data/policy/recovery requirements return to their original owners and reopen affected downstream evidence.

Branches may execute their selected profiles sequentially if they cannot spawn children. The main coordinator's one-additional-skill boundary still applies; absent delegation is not permission for it to load branch skills. Parallel writes require exclusive bounded ownership. The main coordinator retains final authoritative writes unless it explicitly assigns a bounded artifact; shared API and Integration SD ownership stays with it.

## Conflict and decision handling

Use [coordinate changes and consolidate](../SKILL.md#5-coordinate-changes-and-consolidate). Return material contract or cross-branch changes through the branch owner to the main coordinator. Only the main coordinator changes the shared API and records its accepted version. Do not use artifact precedence to hide a contradiction.

## Backend-first contract, then parallel detail

This compatibility anchor now points to the main coordinator's [API definition](../SKILL.md#2-define-the-api-contract), [joint contract review](../SKILL.md#3-review-and-establish-contract-ready) and [parallel branch design](../SKILL.md#4-run-parallel-branch-design). Backend supplies ownership/feasibility evidence and frontend supplies journey feedback; the main coordinator authors and reconciles the contract. Reuse confirmed unchanged contracts and record scope-based `Not Applicable` cases.

## Authoritative write targets

Use the [artifact authorities](../SKILL.md#artifact-authorities). Backend and frontend branches supply consolidated content; the main coordinator assembles the final document set, contract and applicable database/diagram artifacts without duplicating normative content.

## Quality gate

The main coordinator applies its [inline final readiness gate](../SKILL.md#7-apply-the-final-readiness-gate) using branch technical evidence. Branches and specialists may use technical standards and their relevant checklists. They recommend readiness; they do not approve the overall SD set.
