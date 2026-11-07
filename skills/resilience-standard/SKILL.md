---
name: resilience-standard
description: Design, implement, or review bounded failure and recovery behavior, including deadlines, timeouts, cancellation, retries, backoff, jitter, retry budgets, circuit breakers, bulkheads, concurrency limits, queues, backpressure, load shedding, rate limiting, degradation, health checks, recovery, reconciliation, and disaster objectives.
---

# Resilience Standard

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

## Workflow

1. Map critical user journeys, components, dependencies, shared resources, and failure domains.
2. Define SLOs, latency budgets, availability targets, consistency requirements, RPO, RTO, and acceptable degraded modes.
3. Enumerate failures: timeout, refusal, partial response, slow response, overload, stale data, duplicate, reordering, corruption, regional loss, and operator error.
4. Allocate deadlines and cancellation behavior across the call chain.
5. Define retry eligibility, ownership, backoff, jitter, maximum attempts, elapsed budget, and idempotency.
6. Define circuit, bulkhead, concurrency, queue, backpressure, rate-limit, and load-shed controls only where justified.
7. Define fallback, degradation, recovery, reconciliation, failover, and failback.
8. Define health, readiness, liveness, metrics, logs, traces, alerts, runbooks, and control-plane safety.
9. Verify normal, degraded, overload, dependency-loss, recovery, and disaster scenarios.
10. Review against the readiness gate.

## Readiness Gate

Resilience design is implementation-ready only when:

- critical journeys, dependencies, shared resources, failure domains, and SLOs are known;
- deadline and cancellation budgets are allocated end to end;
- retryable outcomes, retry owner, idempotency, backoff, jitter, and budgets are explicit;
- circuit, isolation, queue, overload, and rate controls have thresholds and safe behavior;
- degraded modes and fail-open/fail-closed decisions are approved;
- health probes, recovery, reconciliation, failover, and failback are defined;
- observability, alerts, runbooks, and verification scenarios exist;
- unresolved safety or correctness decisions block affected implementation.

## Reference Routing

- Read [dependency-failure-controls.md](references/dependency-failure-controls.md) for deadlines, cancellation, retries, circuit breakers, bulkheads, and dependency policies.
- Read [overload-health-and-recovery.md](references/overload-health-and-recovery.md) for backpressure, load shedding, rate limits, health probes, degradation, recovery, and disaster behavior.
- Invoke `api-design-standard` for public deadline, cancellation, idempotency, throttling, and error semantics.
- Invoke `error-handling-standard` for typed failures, retry classification, translation, compensation, and terminal handling.
- Invoke `caching-standard` and `messaging-standard` for technology-specific consistency, fallback, replay, and delivery behavior.
- Invoke `logging-standard` and `tracing-standard` for concrete protection, degradation, and recovery telemetry.
- Invoke `software-security-standard` when fail-open behavior, abuse controls, identity, authorization, or sensitive data are involved.

## System Design and SDD Boundary

- In System Design, decide failure model, end-to-end budgets, retry ownership, isolation, overload policy, degraded modes, health semantics, and recovery strategy.
- In SDD, implement approved client settings, policies, concurrency controls, queues, probes, fallbacks, metrics, alerts, runbooks, and tests.
- If implementation reveals a material SLO, failure, safety, retry, isolation, overload, degradation, or recovery change, return it to System Design before coding proceeds.

## Standards Basis

Use official client, protocol, runtime, orchestrator, and dependency documentation. The bundled gRPC and Azure architecture references describe common principles; verify exact behavior for the selected stack.

## Expected Output

Return the dependency and failure model, SLO and time-budget allocation, retry and idempotency policy, circuit and isolation controls, overload and rate policy, degraded modes, health semantics, recovery and disaster plan, observability and runbooks, verification scenarios, assumptions, and unresolved decisions.
