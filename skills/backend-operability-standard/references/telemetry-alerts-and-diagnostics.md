# Telemetry, Alerts, and Diagnostics

## Operational Questions

Begin with questions such as:

- Are critical journeys available and within their latency objective?
- Is demand, rejection, error, or saturation changing materially?
- Which component, dependency, tenant, version, region, or change correlates with impact?
- Is data delayed, duplicated, stale, inconsistent, or unreconciled?
- Is a rollout, configuration change, or dependency event responsible?
- Can operators mitigate safely and verify recovery?

Map each question to the minimum useful signals and a named owner.

## SLIs and SLOs

Define event population, good-event criteria, measurement point, aggregation, window, exclusions, data completeness, target, owner, and review period. Track both user-visible objectives and critical internal leading indicators. Error-budget policy is optional unless adopted by the organization; do not invent one.

## Telemetry and Dashboards

Use metrics for aggregates and trends, traces for request causality and latency, structured logs/events for detailed state and decisions, and audit records for security-relevant actions. Correlate with service, environment, version, region, deployment/change ID, trace/request ID, and bounded domain dimensions.

Avoid unbounded labels, secret or personal data, duplicate signals without purpose, and dashboards with no operational question. Define retention, access, sampling, redaction, cost, and missing-telemetry behavior.

## Alerts

Each alert needs condition, evaluation window, severity, affected objective, likely impact, routing, deduplication/inhibition, owner, response objective, dashboard, runbook, escalation, and test evidence. Prefer symptoms and objective burn or sustained impact over fragile single-instance causes, while retaining cause alerts when immediate action is specific.

Review false positives, false negatives, flapping, pages with no action, and alerts that never fire. A notification is not automatically a page.

## Health and Diagnostics

Separate liveness, readiness, startup, and deep diagnostics. Bound dependency calls and payloads. Protect detailed diagnostics and administrative endpoints. Include build/version, safe config provenance, dependency state, queues/pools, and recent change information only when it helps and does not expose sensitive data.

## Primary References

- [OpenTelemetry Concepts](https://opentelemetry.io/docs/concepts/)
- [Google SRE: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/)
- [Kubernetes Probes](https://kubernetes.io/docs/concepts/workloads/pods/probes/)
