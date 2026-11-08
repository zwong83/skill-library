# SDD Convergence Gate

Run this gate after implementation and before syncing or archiving an OpenSpec change.

## Preconditions

- selected change and schema are known;
- all apply-required artifacts are complete;
- implementation is paused for verification;
- the exact code/configuration/documentation diff is available;
- task status and required test commands are known;
- applicable Test Analysis is `TA-Ready`, or `Not Applicable` has a recorded rationale;
- no secrets or private production data are included in the evidence.

## Checks

### 1. Artifact integrity

- Run `openspec status --change "<change-name>" --json`.
- Run `openspec validate "<change-name>" --type change --strict --no-interactive --json`.
- Confirm proposal, capability specs, design, and tasks are mutually consistent.
- Confirm all material source changes made during implementation were propagated to downstream artifacts.

### 2. Scope integrity

- Compare the actual diff with proposal scope and impact.
- Identify unexplained files, dependencies, interfaces, migrations, configuration, or behavior.
- Confirm out-of-scope behavior was not introduced.

### 3. Requirement coverage

Build a coverage matrix:

| Requirement / Scenario | Design decision | TA case/category/level | Task | Specialist | Test | Implementation | Evidence | Result |
|---|---|---|---|---|---|---|---|---|

Every in-scope requirement and scenario must have implementation and evidence. Every externally visible implementation behavior must trace back to an approved requirement.

### 4. Design conformance

- Verify component/layer boundaries, dependency direction, interfaces, data and transaction ownership, state transitions, error handling, consistency, concurrency, caching, messaging, security, privacy, observability, deployment, migration, rollback, and compatibility against the design delta and applicable approved Backend/Frontend/Integration/contract authorities.
- For frontend scope, verify the approved rendering/routing/module and server/client boundaries; versioned `Contract-Ready` interface; component/design-system contracts; complete UI states; state/data/cache/optimistic/offline behavior; responsive/accessibility/localization support; frontend performance/security/observability/build-delivery decisions; and preservation of authoritative server rules.
- Record any implementation-driven design change in the design artifact and revalidate before accepting it.

### 5. Task authenticity

- Confirm each checked task's deliverables and evidence actually exist.
- For TDD-routed tasks, confirm each claimed cycle has an intended Red failure, Green result, and refactor/broader-suite evidence; test-after implementation is not TDD.
- Confirm every applicable TA case is `Passed`, `Failed`, `Blocked`, or explicitly accepted/excluded with owner and rationale; silent omission is not coverage.
- Verify required unit, integration, contract, UI, system/E2E, performance, security, and regression evidence. Regression cannot pass over a failed required specialist case.
- Reject placeholder implementations, dead code, unexplained TODOs, skipped required tests, and incomplete cleanup.
- Confirm incomplete work remains unchecked and is not hidden in comments or follow-up notes.

### 6. Verification evidence

Run the checks required by the project and change, which may include:

- unit, integration, contract, end-to-end, regression, security, performance, migration, compatibility, and recovery tests;
- frontend format/lint/type/build checks plus component, UI interaction, visual, accessibility, browser/device, contract, journey, performance, security, bundle/artifact, and release-attribution evidence where applicable;
- build, lint, static analysis, type checks, schema validation, and dependency checks;
- manual acceptance, observability, rollout, rollback, or operational-readiness checks.

When applicable, verify structured log fields/severity/correlation/redaction/noise behavior, trace topology/propagation/status/sampling, and the accuracy/actionability of comments and docstrings. Do not accept sensitive telemetry, orphan spans, repeated error logs, stale comments, or TODOs that hide required work.

When applicable, verify architecture dependency rules; error translation, retry, and terminal behavior; cache keys/TTL/invalidation/failure/concurrency; and message contract/delivery/idempotency/ordering/acknowledgement/retry/DLQ/replay behavior. Do not accept vendor exceptions leaking through inward contracts, correctness that depends on cache survival, unbounded retry, acknowledgement before required durable effects, or unsupported exactly-once claims.

When security controls are in scope, apply `software-security-standard` and verify approved authentication and session behavior; server-side use-case/object/tenant/field authorization; authoritative tenant/security-context propagation; negative bypass and isolation scenarios with forbidden-side-effect assertions; duplicate/replay/concurrency/ordering behavior where operations or messages may repeat; data protection and key/secret lifecycle; validation and safe output/error handling; security/audit evidence and sensitive-data exclusions; dependency/build/runtime controls; control-dependency failure behavior; and explicitly owned residual risks. Do not accept UI-only authorization, custom cryptography, secrets in source or telemetry, silent plaintext fallback, or unexecuted security checks reported as passing.

Verify `clean-code-standard` conformance for changed production code: intention-revealing and consistent names, cohesive functions/modules, clear normal flow, explicit dependencies/side effects/nullability/resource ownership, justified duplication/abstraction, language-idiomatic failure handling, and project formatter/linter/type/static/test evidence. Do not force arbitrary size limits, patterns, SOLID interfaces, exceptions, or Java conventions onto languages where they reduce clarity.

Record exact commands or review actions, results, failures, environment limitations, and skipped checks. Do not represent an unexecuted check as passing.

### 7. Unresolved and approval review

- Re-scan source and change artifacts for unresolved material decisions.
- Confirm required owners reviewed security, privacy, data, migration, operations, and release concerns when applicable.
- Confirm any accepted exception is explicit, owned, time-bounded, and outside the claimed completion scope.

## Verdicts

### Converged

Use only when:

- strict validation passes;
- all in-scope requirements and scenarios have passing evidence;
- applicable TA cases are mapped to executed unit, integration, contract, UI, system/E2E, performance, security, regression, or other non-functional evidence, with residual gaps explicitly accepted;
- implementation conforms to the approved design or approved artifact updates;
- all required tasks are genuinely complete;
- no material unresolved item or unexplained drift remains.

### Not Converged

Use when any requirement, evidence, artifact, task, approval, or design-conformance check is missing or failing.

For `Not Converged`:

1. identify the artifact that owns each gap;
2. update that artifact before changing downstream work;
3. add or reopen tasks;
4. implement the correction;
5. rerun the complete convergence gate.

Do not weaken the specification to match an incorrect implementation without explicit product/design authorization.

## Archive handoff

After `Converged`, present:

- convergence verdict and evidence location;
- OpenSpec validation result;
- completed task count;
- delta-spec sync analysis;
- remaining explicitly out-of-scope work;
- requested archive action.

Archive only after the user authorizes it and the OpenSpec archive workflow completes its delta-spec assessment.
