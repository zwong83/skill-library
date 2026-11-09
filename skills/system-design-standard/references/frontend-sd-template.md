# Frontend System Design Template

Use this document for frontend internals and client behavior. Reference Integration SD and machine-readable contracts for server interaction instead of duplicating backend rules or schemas.

## Document control and scope

Record version/status, owner, target release, source/journey/feature IDs, in-scope surfaces, out-of-scope items, support commitments, assumptions, linked Index/Integration/contract versions, and the feature/diagram coverage matrix location.

## 1. Frontend drivers and architecture

Define rendering/hosting strategy, routes/layouts/navigation, feature/module boundaries, server/client boundaries, dependency direction, composition, trust/failure boundaries, and architecture rationale. Include current route/module/data-flow and problem views for brownfield changes plus target route/module/component architecture.

## 2. Components and design system

Define component responsibilities and contracts, composition, variants, slots/content ownership, design-system use, forms/validation presentation, complete UI state model, lifecycle, and test seams. Keep detailed framework code in SDD.

## 3. State and data flow

Define ownership of server, client, URL, form, session, and persistent state; request/data flow; query/cache ownership; invalidation/refresh; optimistic update and rollback; concurrency/staleness; offline/degraded behavior; and recovery. Do not duplicate authoritative business rules or server authorization.

## 4. Per-feature frontend technical logic

Create one visual-first block for every user-facing feature using [feature-diagram-coverage.md](feature-diagram-coverage.md). Require a target route/component/state/data-flow or sequence diagram showing user action, UI state, component ownership, request/event behavior, loading/empty/partial/error/retry/success states, validation, authorization result handling, optimistic update/rollback, navigation, cancellation, recovery, telemetry, and backend contract references as applicable. Brownfield changes also include or link their current behavior and problem IDs.

Adapt the fixed feature construction from the coverage reference: focused UI technical sequence(s), engineering-constraint table, contract/state/data impact table, and error/result/UI-state table. Use compact tables for exact UI rules, support commitments, contract fields/errors, accessibility, performance, security, observability, and verification. Do not narrate the diagrams in long prose.

## 5. Cross-feature journeys and UI behavior

Map approved end-to-end journeys across features, routes, states, transitions, and recovery. Keep feature-specific logic in Section 4.

## 6. Responsive, accessibility, and localization

Define viewport/layout behavior, input modes, supported browsers/devices, keyboard/focus/semantic/assistive-technology behavior, localization/content expansion, time/number/currency handling, theme/contrast, reduced motion, and verification.

## 7. Frontend performance

Define route/asset budgets, rendering and interaction targets, network request/fan-out limits, image/font/code-splitting/caching strategy, memory/long-task controls, RUM measures, regression gates, and evidence. Tie targets to approved commitments or label assumptions.

## 8. Frontend security and privacy

Define content/output handling, session/token boundaries, browser storage, origin/CORS/CSRF/CSP or equivalent policy responsibilities, sensitive-data exposure, dependency/supply-chain controls, abuse considerations, privacy/analytics boundaries, safe failure, and verification. Server security remains authoritative.

## 9. Frontend observability

Define client errors, RUM, journey events, release/source-map handling, correlation with backend traces/logs, privacy/redaction, sampling, dashboards/alerts, ownership, and volume/cost controls. Keep statement-level events/spans in SDD.

## 10. Build, delivery, and rollback

Define reproducible build inputs, artifact identity, public runtime configuration, asset/CDN caching, environment promotion, compatibility, feature exposure, rollout, rollback/forward, source maps, release evidence, and operational ownership.

## 11. Technology decisions and ADRs

Retain only material rendering, framework, module, state, component, experience, performance, security, observability, or delivery decisions whose rationale must survive review.

## 12. Verification and handoff

Map requirement/journey/feature IDs through diagram, route, component, state/data, and contract decisions to component/unit, contract, UI, accessibility, visual, browser/device, performance, security, observability, build, and release evidence. Record frontend implementation prerequisites, dependencies, residual limitations, and Frontend-Ready recommendation.
