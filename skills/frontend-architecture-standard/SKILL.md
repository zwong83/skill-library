---
name: frontend-architecture-standard
description: Design or review web-frontend rendering, routing, feature/module boundaries, server/client execution, dependency direction, composition, SEO, failure boundaries, and conditional microfrontend decisions; use for frontend architecture, not visual styling or backend domain design.
---

# Frontend Architecture Standard

## Input and output contract

This summary follows the detailed workflow and linked gates below. Record source owners, locations/versions and decision status; keep unknowns explicit.

- **Required inputs:** Journeys/surfaces, support targets, backend responsibilities, quality goals and API context.
- **Conditional inputs:** Current routes/modules/hosting and accepted predecessor decisions for affected existing or dependent design.
- **Optional context:** Alternative rendering/architecture examples.
- **Outputs:** Rendering/hosting strategy, route/module/trust maps, dependency rules and verification needs.
- **Destination and consumer:** Use the workflow's existing, requested or documented default artifact/handoff location. Return results to the invoking agent or user for the identified downstream owner; this does not authorize automatic invocation or duplicate artifacts.
- **Completion:** Resolve material architecture/dependency decisions and retain unresolved prerequisites as blockers.


When used by a dedicated frontend design specialist, honor that agent's explicit skill boundary, including transitive references. Route other concerns as evidence or change requests through `frontend-design-agent`; do not load additional skills or take over another specialist's decisions. Standalone use retains the applicable routing below.

Use this skill after user journeys, system boundaries, backend domain ownership, and the draft frontend/backend contract are known.

## Core rules

1. Select SPA, SSR, SSG, incremental/static regeneration, streaming, or hybrid rendering from UX, SEO, freshness, personalization, security, performance, hosting, and operational needs; do not choose by framework habit.
2. Organize by product capability/feature before global technical buckets when it localizes ownership and change. Define allowed dependencies and shared-platform boundaries.
3. Make server/client execution and trust boundaries explicit. Client code and route guards are not authoritative authorization.
4. Define route ownership, layouts, navigation, deep links, redirects, loading/error/not-found boundaries, cancellation, and restoration behavior.
5. Separate domain-neutral UI composition from backend domain authority; do not duplicate pricing, inventory, entitlement, or other authoritative business rules in the browser.
6. Define rendering and hydration boundaries, shared shell, code-splitting units, asset/data dependencies, and failure isolation.
7. Use microfrontends only when independently owned delivery boundaries and operational trade-offs justify their runtime, contract, dependency, consistency, and UX cost.
8. Include public-page metadata, discoverability, canonical/structured information, and crawler behavior only when product requirements make them relevant.

## Workflow

1. Confirm journeys, frontend surfaces, supported environments, backend responsibilities, contract readiness, and quality targets.
2. Choose rendering/hosting and route/module boundaries; record alternatives and trade-offs.
3. Define server/client, feature/shared, trust, error, and release boundaries plus dependency rules.
4. Map critical routes and journeys to components, data needs, loading/failure behavior, observability, and verification.
5. Report decisions, open contract feedback, implementation prerequisites, and residual risks.

## Reference routing

- Read [rendering-routing-and-boundaries.md](references/rendering-routing-and-boundaries.md) for the architecture decision matrix.
- Invoke `frontend-state-data-standard` for state/data ownership and `frontend-component-design-standard` for component contracts.
- Invoke `frontend-performance-standard`, `frontend-security-standard`, and `frontend-build-delivery-standard` only when their concerns affect the architecture.
- Invoke `plantuml-syntax` before creating a frontend component, sequence, state, or deployment diagram.

## Output

Return architecture decision IDs, rendering/hosting strategy, route and module map, server/client and trust boundaries, dependency rules, composition/failure boundaries, SEO/discoverability decisions when applicable, alternatives/trade-offs, contract dependencies, verification intent, and unresolved decisions.
