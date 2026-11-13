---
name: security-testing-standard
description: Plan, execute, or review authorized, non-destructive security verification for approved application controls using code/dependency/configuration analysis and bounded dynamic negative tests; use with a defined target, threat/control baseline, authorization, and safety limits.
---

# Security Testing Standard

Use this skill to verify approved security requirements and controls. It does not authorize testing an unknown target, exploiting company systems, evading controls, persistence, credential attacks, destructive payloads, or unbounded scanning.

## Entry and safety gate

Require the authorized target and owner, environment, time window, source/TA case IDs, threat and control baseline, data classification, permitted techniques/tools, credentials/test identities, rate/concurrency limits, prohibited actions, stop/abort conditions, evidence handling, and incident/escalation contact. Production, shared, external, or third-party targets require explicit scope-specific authorization.

Stop when authorization, ownership, target boundaries, safety controls, expected security behavior, or evidence handling is unclear. Never expose an internal service to a public network, access credential stores, use real secrets unnecessarily, or continue after material instability or out-of-scope impact.

## Core rules

1. Map each test to a threat, abuse case, approved requirement/control, enforcement point, and expected denial/detection/recovery evidence.
2. Prefer the least invasive technique that can prove the control. Demonstrate the minimum necessary evidence; do not pursue exploit chaining, persistence, privilege expansion, data extraction, or service degradation.
3. Cover authentication/session, authorization, object/tenant/field isolation, validation/output safety, sensitive data, cryptography configuration, key/secret handling, audit/privacy, dependency/supply chain, configuration, runtime/deployment, and abuse controls where applicable.
4. Separate SAST, software-composition/dependency analysis, secret scanning, IaC/configuration analysis, DAST, control-specific negative tests, and operational evidence. Tool findings are leads requiring validation and ownership, not automatic confirmed vulnerabilities.
5. For every dynamic case define actor/workload identity, tenant/security context, precondition, invalid or malicious action, expected denial/failure, forbidden side effects, required audit/detection outcome, rate limit, and cleanup.
6. Test positive authorized behavior as well as negative cases so deny-all failures are not mistaken for correct authorization.
7. Use synthetic data and dedicated test identities; mask sensitive evidence and never retain credentials, tokens, keys, personal data, or exploit-ready details beyond approved need.
8. Record tool/version/ruleset, target revision/configuration, suppressions, false-positive rationale, severity method, retest, residual risk, and owner.
9. A scanner pass does not prove complete security, and an unexecuted control check is not passing evidence.
10. Findings are remediated through the owning implementation/design lifecycle; this skill does not silently change requirements, controls, baselines, or risk acceptance.

## Workflow

1. Confirm authorization/safety, scope, assets, threats, controls, TA cases, environment, and evidence boundaries.
2. Build the security verification matrix and choose static, dependency, configuration, dynamic, manual-review, or operational techniques per risk.
3. Execute approved non-destructive checks within rate, data, and stop limits; preserve exact evidence and system health.
4. Validate and deduplicate findings, classify severity/confidence/impact, assign owners, and stop/escalate critical instability or scope breach.
5. Retest authorized fixes and publish coverage, results, limitations, residual risk, and verdict.

## Reference routing

- Read [security-verification-matrix.md](references/security-verification-matrix.md) to map controls and threats to safe techniques and evidence.
- Read [authorization-evidence-and-verdicts.md](references/authorization-evidence-and-verdicts.md) before dynamic execution or release-readiness reporting.
- Invoke `software-security-standard` for the authoritative threat/control architecture and upstream gaps.
- Invoke `backend-api-design-standard`, `db-standard`, `backend-configuration-management-standard`, `log-trace-standard`, or `deployment-release-standard` only for the selected control surface.
- Invoke `contract-testing-standard`, `integration-testing-standard`, or `system-e2e-testing-standard` when security behavior must be verified at that boundary or journey.

## Output

Produce `security-test-report.md` or equivalent approved evidence. Return authorization/scope reference, source/TA/control IDs, target revision/environment, techniques/tools/rulesets, executed cases/results, validated findings and severity/confidence, suppressions/false positives, prohibited/unexecuted checks, system-health/abort events, evidence location/redaction, remediation/retest status, residual risk/owner, and `Security-Passed`, `Security-Failed`, or `Security-Blocked`.
