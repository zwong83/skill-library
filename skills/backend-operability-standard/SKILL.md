---
name: backend-operability-standard
description: Design, implement, or review production operability, including service ownership, SLIs/SLOs, telemetry, dashboards, actionable alerts, health and diagnostics, runbooks, on-call and escalation, incident response, maintenance, support tooling, backup/restore exercises, dependency operations, toil reduction, and operational readiness.
---

# Backend Operability Standard

Use this skill when a service must be monitored, supported, diagnosed, recovered, maintained, or handed to production operators. It governs operating the design; it does not replace resilience controls, logging, or tracing standards.

## Core Rules

1. Assign service, dependency, data, dashboard, alert, runbook, and escalation ownership before production readiness.
2. Start from critical user journeys and operator questions. Collect telemetry that supports decisions, not data without a use.
3. Define SLIs and SLOs with precise populations, windows, exclusions, and owners; do not claim compliance without measurement.
4. Alert on actionable symptoms and imminent objective risk. Every page needs an owner, urgency, response, and validation path.
5. Correlate metrics, logs, traces, events, changes, and business outcomes while controlling cardinality, sensitivity, retention, access, and cost.
6. Keep health endpoints safe, bounded, and aligned with orchestration semantics. Do not expose secrets or trigger restart cascades.
7. Write runbooks for decisions and recovery, including verification and escalation, not only command lists.
8. Design incident declaration, roles, communication, mitigation, evidence preservation, recovery, and learning.
9. Exercise backups, restores, failover, rollback, reconciliation, and critical runbooks; documents alone are not evidence.
10. Track and reduce operational toil, noisy alerts, manual drift, repeated incidents, and unsupported dependencies.
11. Protect operational interfaces and actions with authentication, authorization, audit, rate limits, and safe defaults.

## Workflow

1. Identify critical journeys, service boundaries, owners, dependencies, support model, SLOs, and failure consequences.
2. Define operator questions and map each to SLIs, metrics, logs, traces, events, dashboards, and diagnostics.
3. Define alerts, severity, routing, deduplication, inhibition, escalation, and response objectives.
4. Define health, readiness, startup, maintenance, admin/support, and safe diagnostic interfaces.
5. Create runbooks for alerts, deployment, rollback, dependency failure, capacity, backup/restore, failover, data repair, and security escalation.
6. Define incident roles, communications, evidence, recovery, post-incident learning, and follow-up ownership.
7. Define operational readiness, drills, access, audit, retention, cost, toil, and review cadence.
8. Verify through representative exercises and record gaps.

## Readiness Gate

A service is operationally ready only when:

- ownership, support hours, escalation, dependencies, and service criticality are explicit;
- SLIs/SLOs and critical journey dashboards are defined and measurable;
- alerts are actionable, tested, routed, and linked to runbooks;
- logs, traces, metrics, audits, changes, and business signals correlate safely;
- health and diagnostic behavior is bounded and secure;
- deployment, dependency, capacity, backup/restore, failover, repair, and incident runbooks exist;
- operator access and high-risk actions are least-privileged and audited;
- drills or equivalent evidence validate critical recovery paths;
- known gaps, toil, residual risk, and owners are recorded.

## Reference Routing

- Read [telemetry-alerts-and-diagnostics.md](references/telemetry-alerts-and-diagnostics.md) for operational questions, SLIs/SLOs, telemetry, dashboards, alerts, health, and safe diagnostics.
- Read [runbooks-incidents-and-readiness.md](references/runbooks-incidents-and-readiness.md) for ownership, runbooks, incident response, maintenance, drills, support, and readiness review.
- Invoke `log-trace-standard` for concrete event and span contracts.
- Invoke `backend-resilience-standard` for runtime protection, health semantics, degradation, failover, and reconciliation design.
- Invoke `deployment-release-standard` for deployment/release gates, rollback, feature exposure, and change evidence.
- Invoke `backend-performance-capacity-standard` for capacity indicators, thresholds, forecasts, and saturation response.
- Invoke `software-security-standard` for operational access, audit, incident security, privacy, and protected diagnostics.

## System Design and SDD Boundary

- In System Design, decide ownership, SLO model, operational questions, alert principles, diagnostics, support model, runbook scope, incident process, and readiness evidence.
- In SDD, implement approved telemetry, dashboards-as-code where used, alerts, endpoints, automation, runbooks, drills, and tests.
- Return material SLO, ownership, support, health, security, or recovery-strategy changes to System Design.

## Expected Output

Return service ownership and support model, SLIs/SLOs, telemetry and dashboard plan, alert catalogue, health/diagnostic design, runbook inventory, incident and communication model, maintenance and drill plan, access/audit controls, readiness verdict, toil and risks, assumptions, and unresolved decisions.
