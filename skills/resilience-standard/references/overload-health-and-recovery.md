# Overload, Health, and Recovery

## Overload Control

Protect finite resources before saturation. Combine controls deliberately:

- bounded concurrency limits active work;
- bounded queues absorb short bursts but do not create unbounded latency;
- backpressure slows or rejects upstream producers;
- admission control rejects work unlikely to complete within budget;
- load shedding drops lower-priority or optional work;
- rate limits enforce policy over time and by scope;
- autoscaling adds capacity within known delay and maximum limits.

Define priority, fairness, tenant isolation, burst size, sustained rate, queue capacity, maximum wait, rejection response, and recovery hysteresis. Scaling alone is not overload protection.

## Rate Limiting

Choose a policy such as token bucket, leaky bucket, fixed window, sliding window, or concurrency limit based on burst and fairness requirements. Define scope: global, region, tenant, identity, client, operation, or resource. State consistency requirements for distributed enforcement and behavior when the limiter's own storage is unavailable.

Security and abuse limits may need fail-closed behavior; optional analytics or noncritical limits may permit a controlled fail-open mode. Make that decision explicit.

## Degradation and Fallback

List approved degraded modes with entry trigger, returned data, staleness bound, missing features, authorization behavior, user communication, telemetry, exit condition, and reconciliation. Examples include read-only mode, delayed noncritical work, reduced enrichment, static defaults, or cached non-sensitive data.

Never invent successful business outcomes. Payment, inventory, authorization, entitlement, and destructive operations require explicit treatment of unknown outcomes and reconciliation.

## Health, Readiness, and Liveness

- Liveness answers whether the process should be restarted. Keep it focused on irrecoverable local failure.
- Readiness answers whether the instance should receive new work. Include only dependencies and local conditions whose failure makes useful service impossible.
- Startup checks answer whether initialization is complete when startup may be slow.
- Deep diagnostic checks may inspect dependencies but should not automatically trigger restart cascades.

Define probe timeout, frequency, failure threshold, success threshold, warm-up, drain behavior, and interaction with deployment and autoscaling. Protect diagnostic endpoints and avoid exposing sensitive internals.

## Recovery and Reconciliation

For every partial or unknown outcome define how the system detects, reconciles, retries, compensates, or escalates it. Recovery work needs idempotency, checkpoints, bounds, prioritization, telemetry, and operator controls.

For disaster scenarios define:

- RPO and RTO;
- failure detection and declaration authority;
- failover prerequisites and data consistency;
- traffic switch, dependency order, and capacity;
- failback and divergence reconciliation;
- backup or replica validation;
- exercise schedule and evidence.

## Verification Scenarios

Test representative latency, timeout, refusal, reset, malformed response, partial response, overload, pool exhaustion, queue saturation, retry storm, circuit transition, stale fallback, region or zone loss, recovery, and failback. Verify both protection behavior and business correctness.

## Primary References

- [Azure Reliability Patterns](https://learn.microsoft.com/en-us/azure/well-architected/reliability/design-patterns)
- [Azure Rate Limiting Pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/rate-limiting-pattern)
- [Azure Retry Storm Antipattern](https://learn.microsoft.com/en-us/azure/architecture/antipatterns/retry-storm/)
- [gRPC Health Checking](https://grpc.io/docs/guides/health-checking/)
