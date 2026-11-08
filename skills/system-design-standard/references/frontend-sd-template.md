# Frontend System Design Template

Use this document for frontend internals and client behavior. Reference Integration SD and machine-readable contracts for server interaction instead of duplicating backend rules or schemas.

## Document control and scope

Record version/status, owner, target release, source/journey IDs, in-scope surfaces, out-of-scope items, support commitments, assumptions, and linked Index/Integration/contract versions.

## 1. Frontend drivers and architecture

Define rendering/hosting strategy, routes/layouts/navigation, feature/module boundaries, server/client boundaries, dependency direction, composition, trust/failure boundaries, and architecture rationale. Use focused route, component, or deployment diagrams when useful.

## 2. Components and design system

Define component responsibilities and contracts, composition, variants, slots/content ownership, design-system use, forms/validation presentation, complete UI state model, lifecycle, and test seams. Keep detailed framework code in SDD.

## 3. State and data flow

Define ownership of server, client, URL, form, session, and persistent state; request/data flow; query/cache ownership; invalidation/refresh; optimistic update and rollback; concurrency/staleness; offline/degraded behavior; and recovery. Do not duplicate authoritative business rules or server authorization.

## 4. Journeys and UI behavior

Map approved journeys to routes, states, transitions, loading/empty/partial/error/retry/success behavior, navigation, cancellation, and recovery. Use sequence/state/data-flow diagrams when they clarify material behavior.

## 5. Responsive, accessibility, and localization

Define viewport/layout behavior, input modes, supported browsers/devices, keyboard/focus/semantic/assistive-technology behavior, localization/content expansion, time/number/currency handling, theme/contrast, reduced motion, and verification.

## 6. Frontend performance

Define route/asset budgets, rendering and interaction targets, network request/fan-out limits, image/font/code-splitting/caching strategy, memory/long-task controls, RUM measures, regression gates, and evidence. Tie targets to approved commitments or label assumptions.

## 7. Frontend security and privacy

Define content/output handling, session/token boundaries, browser storage, origin/CORS/CSRF/CSP or equivalent policy responsibilities, sensitive-data exposure, dependency/supply-chain controls, abuse considerations, privacy/analytics boundaries, safe failure, and verification. Server security remains authoritative.

## 8. Frontend observability

Define client errors, RUM, journey events, release/source-map handling, correlation with backend traces/logs, privacy/redaction, sampling, dashboards/alerts, ownership, and volume/cost controls. Keep statement-level events/spans in SDD.

## 9. Build, delivery, and rollback

Define reproducible build inputs, artifact identity, public runtime configuration, asset/CDN caching, environment promotion, compatibility, feature exposure, rollout, rollback/forward, source maps, release evidence, and operational ownership.

## 10. Technology decisions and ADRs

Retain only material rendering, framework, module, state, component, experience, performance, security, observability, or delivery decisions whose rationale must survive review.

## 11. Verification and handoff

Map requirement/journey IDs to frontend decisions and component/unit, contract, UI, accessibility, visual, browser/device, performance, security, observability, build, and release evidence. Record frontend implementation prerequisites, dependencies, residual limitations, and Frontend-Ready recommendation.
