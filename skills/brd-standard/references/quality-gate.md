# BRD Quality Gate

Use this checklist when reviewing or finalizing a BRD. Report `Pass`, `Gap`, or `Needs decision`; do not convert a gap into an invented answer.

## Input readiness

- Mandatory task, project identity, and mode-specific source inputs are present.
- Applicable conditional inputs are supplied or explicitly marked `Not Applicable`.
- Optional context is not treated as a blocker or as stakeholder approval.

## Structure

- Document control identifies project, version, status, date, owner, and reviewers.
- The problem/opportunity, target users, objectives, and intended outcome are explicit.
- Scope contains both inclusions and exclusions, with release boundaries where relevant.
- Functional requirements, business rules, non-functional requirements, data, risks, timeline/deliverables, UAT, and approval control are present or explicitly marked not applicable.
- Interface/integration requirements are present when external systems or vendors are part of the scope.

## Requirement quality

- Every important requirement has a stable ID and a single business intent.
- Requirements are written as observable capabilities or constraints, not implementation tasks.
- Priorities use one defined scheme; status labels are not mixed with priority labels.
- Acceptance criteria are present for critical paths, calculations, state transitions, capacity, payment, privacy, and failure scenarios.
- Duplicate, contradictory, circular, or scope-creeping requirements are identified.

## Decision readiness

- Confirmed facts, proposals, assumptions, and TBC items are distinguishable.
- Open decisions include enough context for a business owner to decide.
- Payment, refund, cancellation, delivery, capacity, customer identity, notification, retention, and compliance policies are not presented as final when pending.
- Approval table names the required approver and current status when known.

## Delivery readiness

- Business rules can be mapped to requirements and UAT scenarios.
- Key customer and operator journeys are covered, including rejection and failure paths.
- Risks and dependencies have impacts and mitigations rather than only labels.
- Release phases and estimates are clearly marked as committed or proposed.
- Release gates cover security, privacy, payments, backups/recovery, operational access, and merchant/customer acceptance where applicable.

## Boundary check

Flag content that belongs in SA/SRS or an implementation plan, including:

- endpoint paths, payload schemas, database DDL, class/module design, framework choices, deployment topology, or detailed algorithms;
- technical mechanisms stated as if they were business approval;
- legal or regulatory conclusions without an appropriate review owner.

Retain the business reason, constraint, expected behavior, or acceptance condition in the BRD and move the mechanism to the appropriate technical artifact.
