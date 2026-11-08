# Dependency Failure Controls

## Dependency Policy

For each dependency record:

- owner, purpose, criticality, and failure domain;
- protocol and operations used;
- latency objective and allocated deadline;
- connection, acquisition, request, idle, and total timeouts where applicable;
- cancellation propagation and cleanup;
- retryable and terminal outcomes;
- idempotency and duplicate behavior;
- concurrency and queue limits;
- circuit and fallback behavior;
- metrics, logs, traces, alerts, and runbook.

## Deadlines and Cancellation

A timeout limits one stage; a deadline limits the remaining end-to-end time. Allocate a caller's budget across network, queue, dependency work, local processing, and response. Downstream work should receive the remaining budget rather than a fresh full timeout.

- Bound connection establishment, pool acquisition, request execution, streaming idle time, and total operation time as the stack permits.
- Propagate cancellation and stop expensive work when the result is no longer useful.
- Reserve enough time for safe cleanup and response translation.
- Do not set every timeout to the same arbitrary value.
- Measure timeout rates and remaining-budget exhaustion by dependency and operation.

## Retries

Retry only when all are true:

1. The failure is plausibly transient.
2. Repetition is idempotent or protected against duplicate side effects.
3. The remaining deadline permits another useful attempt.
4. Added load will not worsen overload.
5. This layer is the designated retry owner.

Use exponential or otherwise increasing backoff with jitter, a small attempt cap, an elapsed-time cap, and a retry budget. Honor server pushback where trustworthy. Do not retry authentication or authorization denial, validation failure, deterministic conflict, permanent absence, or unknown partial success without a specific contract.

Expose original calls, retry attempts, eventual outcomes, and budget exhaustion separately. Test that nested libraries do not silently multiply attempts.

## Circuit Breakers

A circuit breaker can stop repeated calls while a dependency is failing. Define:

- measured outcomes and rolling window;
- minimum volume and open threshold;
- open duration and half-open probe policy;
- concurrency of probes;
- caller-visible error or fallback;
- state scope and distribution;
- metrics, alerting, reset, and operator controls.

Do not use a circuit breaker when ordinary timeouts and bounded concurrency are sufficient, or when an open circuit would hide a correctness-critical operation without recovery.

## Bulkheads and Resource Isolation

Use separate pools, semaphores, workers, partitions, queues, or deployments when one workload can starve another. Define capacity, admission, queue bound, waiting deadline, fairness, rejection behavior, and scaling signal. Isolation has cost; align boundaries with actual criticality and failure domains.

## Failure Translation

Preserve enough cause for observability while returning a stable caller contract. Distinguish timeout, cancellation, throttling, circuit open, capacity rejection, dependency unavailable, conflict, and unknown outcome. Avoid converting every dependency issue into the same retryable error.

## Primary References

- [gRPC Deadlines](https://grpc.io/docs/guides/deadlines/)
- [gRPC Retry](https://grpc.io/docs/guides/retry/)
- [Azure Circuit Breaker Pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker)
- [Azure Bulkhead Pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/bulkhead)
