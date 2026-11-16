# OpenSpec Convergence Evidence Review

Run when the user requests specification conformance review of supplied implementation and verification evidence, usually before synchronization/archive. Do not run implementation, test/build suites, scanners or load tools to fill gaps. OpenSpec artifact validation and read-only inspection of the supplied code/diff are in scope.

## Preconditions

Require a selected change/schema, complete approved artifacts, exact code/configuration/documentation snapshot or diff, current task status and the evidence required by the change's acceptance criteria. Use a supplied Test Analysis matrix when available; equivalent requirement/case traceability is acceptable. Missing required verification yields Not Converged, not an automatic testing invocation.

## Review

1. Validate artifact status and strict OpenSpec conformance using the installed version's supported commands. Confirm proposal, specs, design and tasks agree with approved sources.
2. Compare the supplied snapshot/diff to authorized scope and design/contract versions. Identify unexplained code, dependencies, behavior or material design drift; request decisions from their owners.
3. Build requirement/scenario -> design -> task -> implementation -> case/evidence traceability. Use optional TA IDs where supplied. Inspect whether each claimed result covers its exact scope, revision and environment; do not create new test verdicts from schema validation or code inspection.
4. Check task authenticity. Code deliverables need code evidence; verification tasks need retained observed results. TDD claims need intended Red, Green and refactor evidence. A code-ready handoff cannot close a combined task whose required independent tests remain pending.
5. Review supplied unit/integration/contract/UI/E2E/performance/security/regression and local-check evidence only where required. Preserve failures, stale/missing evidence, skips, flakiness, fidelity limits and justified scope exclusions. No summary overrides a failed required case, and unavailable resources are not Not Applicable.
6. Check unresolved source decisions, approvals, accepted design updates and residual risks. Required gaps cannot be hidden by an exception that does not change the approved scope.
7. Return the coverage/evidence review and Converged or Not Converged, with owners and suggested independent follow-up requests. Re-review affected evidence when sources or snapshots change.

## Verdicts and next action

Converged requires passing artifact validation, complete required task deliverables, trustworthy passing evidence for every required scope, approved design conformance and no material unexplained drift. It is a specification-conformance verdict, not a new testing verdict or deployment approval.

Not Converged identifies missing/failing requirements, tasks, artifacts or evidence. Return requested artifact corrections, implementation fixes or testing work to the user; do not invoke those workflows or implement corrections here. Reopen/update task records only within the requested artifact-edit scope. Never weaken approved behavior merely to match incorrect code.

After Converged, report evidence location, validation, completed tasks, delta/main-spec sync assessment and any explicitly out-of-scope work. Perform synchronization/archive only when explicitly authorized and supported by the observed OpenSpec workflow. Do not report an archive that was not observed.
