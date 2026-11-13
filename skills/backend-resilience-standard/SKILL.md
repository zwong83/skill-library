---
name: backend-resilience-standard
description: Design, implement, or review bounded failure and recovery behavior, including deadlines, timeouts, cancellation, retries, backoff, jitter, retry budgets, circuit breakers, bulkheads, concurrency limits, queues, backpressure, load shedding, rate limiting, degradation, health checks, recovery, reconciliation, and disaster objectives.
---

# Backend Resilience Standard

Use this skill when a system depends on remote services, databases, brokers, caches, shared resources, or capacity-sensitive work, or when failure, overload, degradation, and recovery behavior must be explicit.

## Core Rules

1. Start with criticality, SLOs, dependency map, failure modes, blast radius, consistency needs, and recovery objectives. Do not add resilience patterns by checklist.
2. Bound every remote or blocking operation with a time budget. Propagate deadlines and cancellation where supported.
3. Retry only failures that are transient and operations that are safe to repeat or protected by idempotency. Bound attempts, elapsed time, backoff, jitter, and retry budget.
4. Assign one retry owner across layers. Prevent nested retries and retry storms.
5. Use circuit breakers only when stopping calls creates useful recovery time and a safe open-state behavior exists.
6. Isolate critical resources with bulkheads, bounded concurrency, bounded queues, and separate capacity where failure domains justify it.
7. Apply backpressure, admission control, rate limits, and load shedding before overload exhausts shared resources.
8. Choose fail-open or fail-closed behavior from safety, security, correctness, and business requirements; never from convenience.
9. A fallback must be safer than failure. Do not serve stale authorization, inventory, payment, or other critical truth without explicit acceptance.
10. Health probes must support orchestration decisions without turning every transient dependency issue into a restart cascade.
11. Design recovery, reconciliation, replay, and manual intervention as first-class flows.
12. Instrument every control so operators can distinguish normal protection from hidden failure.

## Mandatory Workflow

**Complete steps 1 through 10 in order for every resilience design, implementation, or review.** Record an outcome for every step. For an existing system, confirm applicable decisions against the approved design and current evidence. Explain each `Not applicable` outcome. Mark a step `Blocked` when a required input or decision is missing and stop dependent work.

1. Identify the affected scope and task mode. Map critical user journeys, components, dependencies, shared resources, and failure domains.
2. Define SLOs, latency budgets, availability targets, consistency requirements, RPO, RTO, and acceptable degraded modes.
3. Identify the failure modes that matter to the scope, including slow or failed dependencies, partial or unknown outcomes, overload, stale or inconsistent data, infrastructure loss, and operator error. For each material failure, identify the affected requirement and shortlist controls using [control selection and reference routing](#control-selection-and-reference-routing).
4. Allocate deadlines and cancellation behavior across the call chain.
5. Decide whether retries are safe and useful for each affected operation. Where selected, define eligibility, ownership, backoff, jitter, maximum attempts, elapsed budget, and idempotency.
6. Select the circuit, isolation, and overload controls that fit the failure and resource constraints. Define applicable thresholds, limits, placement, and rejection behavior.
7. Select safe failure, degradation, and recovery behavior. Define fallback, reconciliation, failover, and failback where the requirements justify them.
8. Define applicable health, readiness, liveness, metrics, logs, traces, alerts, runbooks, and control-plane safety.
9. Specify scenarios and acceptance criteria for the selected controls, covering normal behavior and the relevant failure and recovery paths. For implementation, run the applicable authorized checks. For review, assess the available evidence. Report checks that have yet to run as pending.
10. Apply the readiness gate. Record the decision, evidence, unresolved gaps, and the owner and next action for each blocker.

## Readiness Gate

Claim implementation readiness only after all ten steps have recorded outcomes and the applicable criteria below are satisfied. A blocked step prevents readiness for the affected work.

- critical journeys, dependencies, shared resources, failure domains, and SLOs are known;
- deadline and cancellation budgets are allocated end to end;
- retry eligibility is explicit, including ownership, idempotency, backoff, jitter, and budgets where retries are enabled;
- selected circuit, isolation, queue, overload, and rate controls have thresholds and safe behavior;
- degraded modes and fail-open or fail-closed decisions are approved where applicable;
- health probes, recovery, reconciliation, failover, and failback are defined;
- observability, alerts, runbooks, and verification scenarios exist;
- unresolved safety or correctness decisions block affected implementation.

## Control Selection and Reference Routing

For each material failure, compare plausible controls against the end-to-end time budget, correctness and safety constraints, failure domain, and recovery objectives. Choose the simplest control or combination that satisfies the requirements. An existing control can be retained when evidence shows it is sufficient. Check interactions such as retries adding load, queue wait consuming a deadline, and probes affecting recovery.

Open the reference section that answers the current decision. Once a control is selected, follow the applicable rules in its section and use them as verification criteria. Add another section only when a separate requirement or finding calls for it. Record the failure addressed, rationale, owner, limits or triggers, behavior on activation, and how to verify the control.

| Requirement or failure | Candidate to evaluate | Rules to follow when selected |
|---|---|---|
| Remote or blocking work can exceed its useful time | Deadlines, stage timeouts, and cancellation | [Deadlines and cancellation](references/dependency-failure-controls.md#deadlines-and-cancellation) |
| A transient failure can be retried within budget without duplicate effects | Bounded retries with backoff and jitter | [Retries](references/dependency-failure-controls.md#retries) |
| Sustained dependency failure needs a recovery interval and there is a safe response while calls are blocked | Circuit breaker | [Circuit breakers](references/dependency-failure-controls.md#circuit-breakers) |
| One workload can starve another of shared resources | Separate pools, workers, or other bulkheads | [Bulkheads and resource isolation](references/dependency-failure-controls.md#bulkheads-and-resource-isolation) |
| Finite capacity or traffic bursts threaten useful work | Bounded concurrency or queues, backpressure, admission control, or load shedding | [Overload control](references/overload-health-and-recovery.md#overload-control) |
| Work must be limited over time or by caller, tenant, or operation | Scoped rate limits | [Rate limiting](references/overload-health-and-recovery.md#rate-limiting) |
| A caller must distinguish failure outcomes or know whether work may have succeeded | Stable failure translation | [Failure translation](references/dependency-failure-controls.md#failure-translation) |
| A reduced service can still meet safety and correctness requirements | Fallback or an approved degraded mode | [Degradation and fallback](references/overload-health-and-recovery.md#degradation-and-fallback) |
| Traffic admission, startup, or process restart depends on health | Readiness, startup, or liveness probes | [Health, readiness, and liveness](references/overload-health-and-recovery.md#health-readiness-and-liveness) |
| Partial or unknown outcomes, data loss, or infrastructure failure require recovery | Reconciliation, compensation, restore, or failover and failback | [Recovery and reconciliation](references/overload-health-and-recovery.md#recovery-and-reconciliation) |

- Use [dependency policy](references/dependency-failure-controls.md#dependency-policy) when recording the combined policy for a dependency.
- Use [verification scenarios](references/overload-health-and-recovery.md#verification-scenarios) for the failure paths covered by step 9.
- Invoke `backend-api-design-standard` for public deadline, cancellation, idempotency, throttling, and error semantics.
- Invoke `exception-error-standard` for typed failures, retry classification, translation, compensation, and terminal handling.
- Invoke `cache-standard` for cache consistency or fallback and `message-standard` for broker replay or delivery behavior when the respective dependency is in scope.
- Invoke `log-trace-standard` for concrete protection, degradation, and recovery telemetry.
- Invoke `software-security-standard` when fail-open behavior, abuse controls, identity, authorization, or sensitive data are involved.

## System Design and SDD Boundary

- In System Design, decide failure model, end-to-end budgets, retry ownership, isolation, overload policy, degraded modes, health semantics, and recovery strategy.
- In SDD, implement approved client settings, policies, concurrency controls, queues, probes, fallbacks, metrics, alerts, runbooks, and tests.
- If implementation reveals a material SLO, failure, safety, retry, isolation, overload, degradation, or recovery change, return it to System Design before coding proceeds.

## Standards Basis

Use official client, protocol, runtime, orchestrator, and dependency documentation. The bundled gRPC and Azure architecture references describe common principles; verify exact behavior for the selected stack.

## Expected Output

Return a numbered record of the ten workflow outcomes. For each affected failure, record the requirement, selected controls and rationale, operating limits, owner, and verification evidence or pending checks. For a full design, include the dependency and failure model, budgets, recovery and degraded behavior, observability, runbooks, and readiness verdict.
