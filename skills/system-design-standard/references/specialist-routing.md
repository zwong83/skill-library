# System Design Specialist Routing

The main `system-design-agent` owns the shared API and delegates to [Backend Design](../../../agents/backend-design-agent/SKILL.md) (`backend_design`) and [Frontend Design](../../../agents/frontend-design-agent/SKILL.md) (`frontend_design`). It follows its inline workflow and does not load this reference. Both branches review affected contracts before detailed design from the accepted version.

## Ordered backend stages

Establish approved quality/security/recovery constraints before the first stage. In contract-review, apply only the bounded review portion of applicable stages, including identity/access and public-error semantics; do not require full detailed artifacts. In detailed design, pass accepted predecessor decisions forward in this order:

| Order | Concern and owner | Specialist | Codex adapter |
|---|---|---|---|
| 1 | Stack, module/layer architecture, data models, DDL/DML, transactions, access paths and migration/recovery | [Architecture](../../../agents/architecture-agent/SKILL.md) | `architecture` |
| 2 | Authentication, principal/session/token lifecycle, permissions and enforcement | [Identity/Access](../../../agents/identity-access-agent/SKILL.md) | `identity_access` |
| 3 | Applicable cache/message behavior and dependency failure controls | [Middleware](../../../agents/middleware-engineering-agent/SKILL.md) | `middleware_engineering` |
| 4 | Logs/traces, error taxonomy, exception propagation, correlation and troubleshooting | [Diagnostics](../../../agents/diagnostics-agent/SKILL.md) | `diagnostics` |
| Conditional before final review | Configuration/secrets delivery, deployment/release and operational support | [Delivery/Operations](../../../agents/delivery-operations-agent/SKILL.md) | `delivery_operations` |
| 5, final review | Assess cross-cutting quality against the initial constraints and stage evidence | [Quality Attributes](../../../agents/quality-attributes-agent/SKILL.md) | `quality_attributes` |

Classify each stage as required, conditional or not applicable with source IDs and reasons. These are ordered sibling assignments owned by the backend coordinator, not a chain of nested spawns. Only affected scopes may proceed independently once their own prerequisites are satisfied. The frontend coordinator uses the dedicated ordered stages below.

## Ordered frontend stages

Capture approved experience, support, security/privacy, performance, telemetry and release constraints before Architecture starts. Apply bounded review portions in contract-review; detailed design requires the accepted contract or justified unchanged/no-API disposition. Before dependent architecture/components, confirm an accepted UX baseline or assign the existing Experience agent a bounded `ux-baseline` phase when needed. That phase uses installed `ui-ux-pro-max` for proposals and `frontend-experience-standard` for constraints, without requiring downstream designs. Record reuse, proposal/acceptance status and owner decisions. The later `experience-detail` phase consumes the accepted baseline and stage outputs. These passes use the same specialist, not an extra depth level. The four dedicated agents are siblings spawned by the frontend coordinator:

| Order | Concern and owner | Specialist | Codex adapter |
|---|---|---|---|
| Before architecture, when needed | Missing or revised visual/interaction baseline | [Frontend Experience](../../../agents/frontend-experience-agent/SKILL.md), `ux-baseline` phase | `frontend_experience` |
| 1 | Frontend stack, rendering, routes, modules and execution boundaries | [Frontend Architecture](../../../agents/frontend-architecture-agent/SKILL.md) | `frontend_architecture` |
| 2 | Component contracts, forms, state ownership, API flows and recovery | [Components and State](../../../agents/frontend-component-state-agent/SKILL.md) | `frontend_component_state` |
| 3 | Responsive, accessible, localized and supported UI behavior | [Frontend Experience](../../../agents/frontend-experience-agent/SKILL.md) | `frontend_experience` |
| 4 | Client performance/security/telemetry, build/release and final client quality review | [Quality and Delivery](../../../agents/frontend-quality-delivery-agent/SKILL.md) | `frontend_quality_delivery` |

Classify applicability with source evidence; pass accepted predecessor revisions forward, return findings to original owners and revalidate affected downstream results. The final stage uses the original approved constraints, not newly invented targets. Same-scope stages follow this order; independent scopes may continue once prerequisites are met. Each agent owns its mandatory workflow and skill boundary. Diagram authors may use their explicitly allowed `plantuml-syntax`. Shared API and cross-branch decisions remain with the main coordinator.

## Ownership and feedback

Every selected agent returns diagram-first technical content under the main coordinator's [presentation policy](../../../agents/system-design-agent/SKILL.md#mandatory-diagram-first-presentation). Assign relevant visual coverage before drafting supporting words; final quality review checks actual section order, required views and their consistency. Existing skill allowlists still apply.


- Architecture's only skills are languages/engines, backend layering and database design, in that order. Architecture owns all database artifacts, including later identity/session/permission and outbox/inbox/deduplication revisions.
- Identity/Access uses authentication then authorization standards and owns those policies and enforcement decisions. Return public security-scheme/header/cookie/denial changes through the main API owner.
- Middleware uses cache, message and backend-resilience standards in order as applicable. No cache or broker is introduced without a requirement; resilience may still apply to database/HTTP dependencies. It supplies recovery and diagnostic requirements without taking over log/trace/error design.
- Diagnostics uses log/trace then exception/error guidance. It reconciles the two outputs and consumes the established recovery policy instead of assigning another retry owner. Public error changes return to the API owner.
- Delivery consumes identity, middleware and diagnostic contracts and owns their operational realization. It is conditional but required when deployment/configuration/support concerns affect the assignment.
- Quality reviews the initial constraints against the assembled results. It identifies gaps and owners, not competing designs or newly invented targets. Return material findings to the owner, update affected downstream evidence and repeat affected quality checks.
- The main coordinator alone reconciles shared API changes and `Contract-Ready`. Accepted version/hash and changed decision IDs must accompany revised assignments. Unresolved material changes block affected readiness.
- Each feature's technical-flow diagram and each conditional view has one owner and authoritative target. Restricted specialists use their allowed skills, existing diagram conventions and installed syntax/render tools; they do not load additional diagram skills through a reference. Required diagram and validation evidence remains part of their handoff.
- Respect actual shared depth/concurrency limits and exclusive write ownership. Use a general-purpose subagent with the explicit workflow path if a named adapter is unavailable; a branch may apply profiles sequentially when it cannot spawn further. The main coordinator's one-additional-skill boundary remains in force.
- Branches return consolidated technical evidence. The main coordinator applies its inline final gate and writes the accepted SD set, preserving contract, data, integration and branch authority boundaries.
