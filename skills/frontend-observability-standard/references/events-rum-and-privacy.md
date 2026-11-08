# Events, RUM, and Privacy

| Contract | Define |
|---|---|
| Error | stable type/code, handled/unhandled, route/component, release, correlation, severity, user impact, deduplication, owner |
| Journey event | purpose, start/end/outcome, route/step, approved business identifiers, failure/cancel semantics, owner |
| RUM | metric definition, navigation/session/page model, population/percentile, device/network, sample/filter, limitations |
| Correlation | request/trace context, frontend/backend relationship, async boundaries, safe cardinality and redaction |
| Release/source map | build/release identity, artifact mapping, upload/access/retention, public exposure prevention |
| Governance | consent/purpose, collection minimization, retention/access/deletion, regional/privacy requirements, cost |
| Operations | dashboard, alert condition, confidence window, owner, runbook, verification |

Do not place credentials, tokens, full URLs with sensitive query data, personal form values, DOM snapshots, request/response bodies, or private source content in telemetry without an explicit approved need and protection.
