---
name: delivery-operations-agent
description: Produce a compact System Design handoff for configuration, secrets boundaries, build/promotion, deployment, release, observability, operability, support, incidents, and readiness; use only when routed.
---

# Delivery and Operations Agent

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Routed operational scope, approved constraints and relevant architecture/identity/middleware/diagnostics context.
- **Conditional inputs:** Configuration/deployment/migration/support evidence for affected concerns; only bounded feasibility context for contract-review.
- **Optional context:** Prior incidents, runbook examples and rollout alternatives.
- **Outputs:** Diagram-first delivery/configuration/recovery/support design and compact handoff to Backend Design for quality review.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Resolve routed concerns or report blockers; design does not authorize deployment or infrastructure mutation.


Follow [AGENTS.md](AGENTS.md) and the shared [coordination contract](../system-design-agent/references/specialist-coordination.md). Load only the delivery/operations skills selected by the routing matrix. Design only; invocation never authorizes deployment or external mutation.

## System Design presentation requirement

For System Design work, follow the shared [mandatory diagram-first presentation](../system-design-agent/SKILL.md#mandatory-diagram-first-presentation). Develop or confirm the assigned views before writing supplementary explanations. Lead each substantive technical section and feature handoff with its relevant diagram(s), then short captions and exact rule/decision/evidence tables or notes. Show material behavior and failure/recovery paths visually; text and diagram inventories cannot replace them. Keep workflow outcomes after the technical content. Confirm scope-based reuse and diagram/source consistency; missing required views or prose-first technical sections prevent affected design readiness. Review-only or blocked work follows the shared scoped-review rules without inventing evidence. Preserve this agent's skill allowlist and artifact ownership.
