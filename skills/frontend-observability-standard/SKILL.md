---
name: frontend-observability-standard
description: Design, implement, or review frontend error capture, real-user monitoring, journey events, client/server correlation, release attribution, source-map symbolication, sampling, privacy, analytics, dashboards, alerts, and diagnostic evidence.
---

# Frontend Observability Standard

Use this skill when frontend behavior must be diagnosed, measured, correlated, or operated after delivery.

## Core rules

1. Start from operational and product questions; do not collect every click, exception, DOM value, or payload by default.
2. Define event/error names, route/journey, release/build, environment, correlation/trace context, outcome, severity, timing, and ownership consistently.
3. Capture handled/unhandled errors, promise rejections, route/render failures, API/dependency failures, resource failures, and degraded states without duplicate reporting.
4. Correlate frontend activity with backend requests/traces using approved context that excludes credentials, personal data, and unsafe high-cardinality fields.
5. Define RUM metrics/populations/percentiles, sampling, bot/internal filtering, session/page/navigation semantics, consent, retention, access, cost, and data-quality limitations.
6. Govern source maps by artifact identity, symbolication access, retention, upload timing, and public exposure; do not publish sensitive sources accidentally.
7. Separate product analytics, experimentation, security/audit, and operational telemetry when purpose, consent, access, or retention differs.
8. Tie dashboards and alerts to actionable owners and runbooks; avoid alerting on raw client noise without impact and confidence.

## Workflow

1. Identify journeys, SLIs/questions, failure modes, data classification, consent, ownership, release process, and correlation needs.
2. Define event/error/RUM contracts, sampling/privacy, release/source-map, dashboards/alerts, and verification.
3. Map required instrumentation to routes/components/API clients and keep statement-level placement for SDD.
4. Report observability gaps, data-quality limitations, cost, and residual risk.

## Reference routing

- Read [events-rum-and-privacy.md](references/events-rum-and-privacy.md) for the event/RUM/privacy decisions written into Frontend SD.
- Invoke `log-trace-standard` for shared event and trace correlation rules.
- Invoke `frontend-performance-standard` for user-performance metrics and `frontend-security-standard` for sensitive-data exclusions.

## Output

Return operational questions/SLIs, event/error/RUM schemas, correlation and release identity, source-map policy, sampling/filtering/privacy/retention/access rules, dashboards/alerts/runbooks, instrumentation ownership, verification, costs/limitations, and unresolved decisions.
