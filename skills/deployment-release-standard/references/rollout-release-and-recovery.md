# Rollout, Release, and Recovery

## Strategy Selection

| Strategy | Suitable when | Key requirements |
|---|---|---|
| Recreate | Downtime is accepted or exclusivity is required | Explicit outage and recovery plan |
| Rolling | Mixed versions are compatible and gradual instance replacement is sufficient | Surge/unavailable capacity, readiness, drain, rollback compatibility |
| Canary | Risk should be tested on limited representative traffic | Traffic control, sample validity, guardrails, promotion/abort automation |
| Blue-green | Fast environment switch and capacity duplication are acceptable | Data compatibility, traffic switch, warm-up, old-environment retention |
| Feature-controlled | Code deployment should be separated from user exposure | Safe default, targeting, audit, kill switch, expiry and cleanup |

Combinations are valid but add states and operational complexity.

## Rollout Contract

Define:

- preconditions and change window;
- target scope, batches, interval, and maximum unavailable/surge;
- startup, readiness, liveness, drain, and graceful shutdown;
- exposure and targeting rules;
- success and guardrail metrics with evaluation windows;
- pause, abort, promotion, completion, and operator override;
- post-deploy smoke, synthetic, business, and reconciliation checks;
- notifications, ownership, evidence, and cleanup.

Canary analysis must account for low traffic, tenant/user skew, time-of-day effects, cold start, cache state, and dependency differences.

## State and Migration

Sequence application, schema, backfill, configuration, broker, cache, and infrastructure changes explicitly. Preserve mixed-version operation for the rollout window. Separate reversible application rollout from irreversible data change and state the roll-forward repair path.

## Feature Release

Define flag owner, purpose, type, default, evaluation context, privacy, targeting, exposure metric, provider-failure behavior, staged percentages/cohorts, approval, kill switch, expiry, and code/config cleanup. Never use a flag as the only authorization control.

## Recovery

Choose rollback, roll-forward, disablement, traffic shift, restore, compensation, or reconciliation according to the actual state. Define the latest safe decision point, time objective, data impact, validation, and authority. Exercise recovery before relying on it.

## Primary References

- [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Kubernetes Canary Deployment](https://kubernetes.io/docs/tutorials/stateless-application/canary-deployment/)
- [Kubernetes Probes](https://kubernetes.io/docs/concepts/workloads/pods/probes/)
- [OpenFeature Specification](https://openfeature.dev/specification/)
