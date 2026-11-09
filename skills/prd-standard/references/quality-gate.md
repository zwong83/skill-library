# PRD Quality Gate

Report each check as `Pass`, `Gap`, or `Needs decision`.

## Input readiness

- Mandatory task, product identity, and mode-specific source inputs are present.
- Applicable conditional inputs are supplied or explicitly marked `Not Applicable`.
- Optional context is not treated as a blocker or as product approval.

## Product clarity

- Overview identifies the product/feature, target release, and value proposition.
- Problem statement names affected users, current pain or opportunity, evidence, and urgency.
- Target users are specific enough to guide behavior and UX; unsupported persona details are marked as assumptions.
- Goals are outcomes, not feature lists, and success metrics have definitions and targets or explicit TBD status.

## Scope and prioritization

- P0/P1/P2 meanings are defined and used consistently.
- In-scope and out-of-scope boundaries are explicit.
- Functional requirements map to user stories and a stated goal.
- Dependencies, milestones, and release boundaries are visible.
- Each approved source item has a documented operation-level mapping or a source-based deferred/inapplicable disposition for the selected release. Review coverage separately from document structure.

## Requirement quality

- Critical stories and requirements have stable IDs.
- Each important requirement describes one observable behavior or constraint.
- An umbrella capability is not marked covered unless its applicable actor actions and system outcomes can be traced to acceptance criteria.
- Acceptance criteria cover normal, validation, permission, empty, failure, and boundary cases as relevant.
- UI/UX requirements describe behavior, not only visual taste.
- NFRs are measurable or marked proposed.
- Duplicate, contradictory, or circular requirements are identified.

## Decision readiness

- Facts, research, assumptions, proposals, and pending approvals are distinguishable.
- Open questions contain enough context for a decision-maker to answer.
- Product policy decisions are not hidden inside technical details.
- Approval status and release acceptance criteria are present when the document is used for execution.

## AI-coding readiness

- The document is Markdown-friendly and scannable.
- Build order is explicit where sequencing matters.
- Ambiguous behavior is resolved or marked as a blocking decision.
- The document does not ask an AI agent to guess a framework, API, schema, or security policy.
- Technical considerations are clearly separated into confirmed constraints, proposals, or a linked SA/SRS.

## Boundary and safety check

Flag content that belongs in a technical artifact, including endpoint contracts, database DDL, file/class design, detailed algorithms, deployment topology, or unapproved technology choices. Retain the product-level constraint or desired behavior in the PRD and move the implementation mechanism elsewhere.
