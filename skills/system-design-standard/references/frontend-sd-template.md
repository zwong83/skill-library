# Frontend System Design Template

Use this document for frontend internals and client behavior. Reference Integration SD and machine-readable contracts for server interaction instead of duplicating backend rules or schemas.

## Required presentation order

After compact document-control metadata, the first technical content must be the overview diagram. Every substantive section below starts with its specified visual, then a short caption, then supplementary exact rules, rationale, constraints and evidence. This order is mandatory; do not start with narrative or a specification table. Reuse an authoritative diagram or focused excerpt when it already answers the section's question, with one maintained source. Embed a readable preview, or inline readable source with a rendering limitation when previews cannot be produced. A bare link or placeholder is insufficient. Use source-based `Not Applicable` only for truly unaffected sections; retain exact schemas/SQL and administrative records in their proper formats.

## Document control and scope

Record version/status, owner, target release, source/journey/feature IDs, in-scope surfaces, out-of-scope items, support commitments, assumptions, linked Index/Integration/contract versions, and the feature/diagram coverage matrix location.

## 1. Frontend drivers and architecture

**Diagram first:** Present route/module/server-client architecture and primary journey flow; distinguish current/problem and target views for brownfield scope. Follow with only the details the visuals cannot express precisely.

Define rendering/hosting strategy, routes/layouts/navigation, feature/module boundaries, server/client boundaries, dependency direction, composition, trust/failure boundaries, and architecture rationale. Include current route/module/data-flow and problem views for brownfield changes plus target route/module/component architecture.

## 2. Components and design system

**Diagram first:** Present component composition and variant/state diagrams, with applicable annotated wireframes before contract/token tables. Follow with only the details the visuals cannot express precisely.

Define component responsibilities and contracts, composition, variants, slots/content ownership, design-system use, forms/validation presentation, complete UI state model, lifecycle, and test seams. Keep detailed framework code in SDD.

## 3. State and data flow

**Diagram first:** Present state ownership and query/mutation/data-flow diagrams showing cancellation, stale responses and recovery. Follow with only the details the visuals cannot express precisely.

Define ownership of server, client, URL, form, session, and persistent state; request/data flow; query/cache ownership; invalidation/refresh; optimistic update and rollback; concurrency/staleness; offline/degraded behavior; and recovery. Do not duplicate authoritative business rules or server authorization.

## 4. Per-feature frontend technical logic

**Diagram first:** Present each feature's route/component/state/data-flow or sequence diagram before exact UI/contract rules. Follow with only the details the visuals cannot express precisely.

Create one visual-first block for every user-facing feature using [feature-diagram-coverage.md](feature-diagram-coverage.md). Require a target route/component/state/data-flow or sequence diagram showing user action, UI state, component ownership, request/event behavior, loading/empty/partial/error/retry/success states, validation, authorization result handling, optimistic update/rollback, navigation, cancellation, recovery, telemetry, and backend contract references as applicable. Brownfield changes also include or link their current behavior and problem IDs.

Adapt the fixed feature construction from the coverage reference: focused UI technical sequence(s), engineering-constraint table, contract/state/data impact table, and error/result/UI-state table. Use compact tables for exact UI rules, support commitments, contract fields/errors, accessibility, performance, security, observability, and verification. Do not narrate the diagrams in long prose.

## 5. Cross-feature journeys and UI behavior

**Diagram first:** Present end-to-end journey/navigation and recovery-state diagrams. Follow with only the details the visuals cannot express precisely.

Map approved end-to-end journeys across features, routes, states, transitions, and recovery. Keep feature-specific logic in Section 4.

## 6. Responsive, accessibility, and localization

**Diagram first:** Present responsive layout/wireframe and focus/interaction flows with applicable locale/RTL adaptations before support matrices. Follow with only the details the visuals cannot express precisely.

Define viewport/layout behavior, input modes, supported browsers/devices, keyboard/focus/semantic/assistive-technology behavior, localization/content expansion, time/number/currency handling, theme/contrast, reduced motion, and verification.

## 7. Frontend performance

**Diagram first:** Present critical route loading/render/interaction flows with resource and budget annotations. Follow with only the details the visuals cannot express precisely.

Define route/asset budgets, rendering and interaction targets, network request/fan-out limits, image/font/code-splitting/caching strategy, memory/long-task controls, RUM measures, regression gates, and evidence. Tie targets to approved commitments or label assumptions.

## 8. Frontend security and privacy

**Diagram first:** Present browser/server trust and session/storage/content-flow diagrams with enforcement and privacy boundaries. Follow with only the details the visuals cannot express precisely.

Define content/output handling, session/token boundaries, browser storage, origin/CORS/CSRF/CSP or equivalent policy responsibilities, sensitive-data exposure, dependency/supply-chain controls, abuse considerations, privacy/analytics boundaries, safe failure, and verification. Server security remains authoritative.

## 9. Frontend observability

**Diagram first:** Present client event/error/correlation flows through permitted telemetry sinks. Follow with only the details the visuals cannot express precisely.

Define client errors, RUM, journey events, release/source-map handling, correlation with backend traces/logs, privacy/redaction, sampling, dashboards/alerts, ownership, and volume/cost controls. Keep statement-level events/spans in SDD.

## 10. Build, delivery, and rollback

**Diagram first:** Present build/artifact/deployment topology and rollout/mixed-version/rollback sequences. Follow with only the details the visuals cannot express precisely.

Define reproducible build inputs, artifact identity, public runtime configuration, asset/CDN caching, environment promotion, compatibility, feature exposure, rollout, rollback/forward, source maps, release evidence, and operational ownership.

## 11. Technology decisions and ADRs

**Diagram first:** Present the relevant decision-impact route/component/state view or focused excerpt before compact ADR notes; reuse authoritative sources. Follow with only the details the visuals cannot express precisely.

Retain only material rendering, framework, module, state, component, experience, performance, security, observability, or delivery decisions whose rationale must survive review.

## 12. Verification and handoff

**Diagram first:** Present a journey/component verification-boundary view before coverage, evidence and readiness tables. Follow with only the details the visuals cannot express precisely.

Map requirement/journey/feature IDs through diagram, route, component, state/data, and contract decisions to component/unit, contract, UI, accessibility, visual, browser/device, performance, security, observability, build, and release evidence. Record frontend implementation prerequisites, dependencies, residual limitations, and Frontend-Ready recommendation.
