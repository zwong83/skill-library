# Runbooks, Incidents, and Readiness

## Ownership and Support

Record service owner, technical owner, data owner, on-call/support route, coverage hours, dependency contacts, escalation path, severity model, and communication channels. Do not infer continuous support when staffing or agreement is absent.

## Runbook Contract

Every critical runbook should include:

- trigger, scope, risk, prerequisites, and required authority;
- user/business impact and affected objectives;
- diagnosis and decision points;
- safe mitigation with stop conditions;
- rollback, roll-forward, restore, or reconciliation choices;
- verification of technical and business recovery;
- escalation and communication;
- evidence to preserve and follow-up work;
- owner, last exercise, and next review.

Avoid embedding credentials, sensitive production values, or destructive commands without safeguards and authorization boundaries.

## Incident Lifecycle

Define detection, declaration, severity, incident command, technical response, communications, security/privacy escalation, mitigation, recovery, validation, closure, and learning. Preserve a timeline and decision evidence. Post-incident review should focus on system conditions and actionable prevention, with owners and dates for follow-up.

## Operational Readiness Review

Review ownership, dependencies, SLOs, dashboards, alerts, logs/traces, deployment/rollback, configuration, capacity, security, backup/restore, failover, reconciliation, data repair, support tooling, runbooks, access, documentation, and known risks. Mark each `Ready`, `Gap`, `Risk accepted`, or `Not applicable` with evidence and owner.

## Exercises and Maintenance

Exercise the highest-risk recovery paths at a cadence justified by change and criticality. Validate backups by restore, not existence. Track certificate/secret expiry, dependency end-of-life, storage growth, queue/backlog, scheduled jobs, schema cleanup, feature-flag cleanup, and alert/runbook drift.

Measure toil and repeated manual work. Automate only after the safe decision process is understood and observable.

## Primary References

- [Google SRE Workbook: Monitoring](https://sre.google/workbook/monitoring/)
- [Google SRE: Launch Coordination Checklist](https://sre.google/sre-book/launch-checklist/)
- [Google SRE: Managing Incidents](https://sre.google/sre-book/managing-incidents/)
