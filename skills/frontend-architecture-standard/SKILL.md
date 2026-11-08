---
name: frontend-architecture-standard
description: Design or review web-frontend rendering, routing, feature/module boundaries, server/client execution, dependency direction, composition, SEO, failure boundaries, and conditional microfrontend decisions; use for frontend architecture, not visual styling or backend domain design.
---

# Frontend Architecture Standard

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
