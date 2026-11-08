# Apply Workflow

Use only after source readiness, complete apply-required artifacts, strict validation, applicable `TA-Ready` analysis, and explicit implementation authorization.

## Entry

1. Run the active OpenSpec apply-instructions command for the selected change.
2. Validate the structured response and read every returned context file.
3. Confirm task scope, approved System Design constraints, current code/test baseline, evidence location, and authorization boundary.
4. Confirm TA case IDs, positive/negative/boundary coverage, test-level/specialist allocation, specialist prerequisites/outputs, and TDD routing for behavior-changing tasks.
5. Stop if instructions, required artifacts, TA, source status, or design constraints conflict.

## Task execution

- Implement one bounded approved task at a time.
- Invoke `clean-code-standard` for production-code work.
- Invoke `tdd-standard` through `tdd-agent` when TDD is routed for the task.
- Load only the technical skills activated by the task routing matrix:

| Changed concern | Conditional skill |
|---|---|
| Module/layer/object/pattern | `layered-architecture-standard`, conditional OOD/SOLID/patterns |
| API/service contract mapping | `api-design-standard` |
| Persistence/transactions/migrations | `database-persistence-standard` |
| Resilience behavior | `resilience-standard` |
| Configuration/secrets/flags | `configuration-management-standard` |
| Performance/capacity implementation | `performance-capacity-standard` |
| Deployment/release artifacts | `deployment-release-standard` |
| Operability/telemetry/runbooks | `operability-standard`, conditional logging/tracing |
| Security controls | `software-security-standard` |
| Errors | `error-handling-standard` |
| Cache | `caching-standard` |
| Messaging | `messaging-standard` with only the selected broker reference |
| Test portfolio/evidence | `testing-strategy-standard` |
| Test analysis | `test-analysis-standard` |
| Unit/component tests | `unit-testing-standard` |
| Integration boundaries | `integration-testing-standard` |
| Provider/consumer compatibility | `contract-testing-standard` |
| UI behavior, visual, accessibility, compatibility | `ui-testing-standard` |
| Critical multi-component journeys | `system-e2e-testing-standard` |
| Authorized security control verification | `security-testing-standard` |
| Cross-level regression | `regression-testing-standard` |
| Red-Green-Refactor | `tdd-standard` |
| Non-obvious comments/contracts | `code-comments` |

These skills map and verify approved decisions; they do not authorize a new strategy. Escalate material architecture, contract, ownership, consistency, security, recovery, deployment, operational, or test-strategy changes to System Design or the owning requirements artifact.

## Verification and evidence

Run project-required formatting, lint, type/static analysis, build, tests, and task-specific checks. Record exact commands, versions where relevant, results, failures, retries, skips, and limitations. Never report an unexecuted check as passing.

For non-TDD work, route assigned cases to the applicable unit, integration, contract, UI, system/E2E, performance, or security testing Agent after its prerequisites and authorization gates pass. Route required cross-level regression to `regression-testing-agent` after a testable target and specialist evidence exist.

Mark a task complete only after its code and required specialist tests, migration checks, documentation, telemetry, and evidence are complete. Routine task-status and evidence updates inside the selected change are part of authorized Apply; upstream changes, main-spec synchronization, archive, Git operations, deployment, and unrelated changes are not.

Stop on ambiguity, failed prerequisites, design drift, out-of-scope impact, or unresolved security/operational concerns. Correct the artifact that owns the decision through its authorized mode before resuming.
