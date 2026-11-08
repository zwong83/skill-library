# Testing, Capacity, and Regression

## Test Types

| Test | Decision it supports |
|---|---|
| Benchmark | Cost or throughput of a focused component or algorithm |
| Load | Behavior at expected normal and peak demand |
| Stress | Breaking point, limiting resource, and overload behavior |
| Spike | Response to sudden demand and autoscaling delay |
| Soak | Leaks, fragmentation, drift, and long-duration degradation |
| Scalability | Throughput/latency efficiency as resources or partitions increase |
| Failover capacity | Whether remaining capacity meets degraded objectives during loss |

Define environment, version, topology, dataset, generators, generator headroom, warm-up, duration, repetitions, cache state, success criteria, abort limits, and result retention. Validate the load generator is not the bottleneck.

## Capacity and Headroom

Capacity planning should include:

- measured service demand and sustainable throughput at the target SLO;
- resource and dependency quotas at the limiting point;
- traffic/data growth and forecast uncertainty;
- rollout surge, maintenance, backup, compaction, and batch work;
- zone/region/node/dependency failure scenarios;
- autoscaling trigger, observation window, provisioning lag, minimum/maximum, and cooldown;
- cost and overprovisioning trade-offs.

Document usable capacity, not theoretical maximum. Preserve headroom before saturation and validate that scale-out actually relieves the limiting resource.

## Regression Evidence

Compare the same scenario, dataset, environment, instrumentation, and statistical method to an accepted baseline. Define thresholds for latency, throughput, errors, and resource cost. Treat noisy or inconclusive results as inconclusive, not passing.

Production guardrails should detect sustained changes in user-visible latency, traffic, errors, saturation, queueing, dependency behavior, and cost. Tie alerts to an action and owner.

## Primary References

- [Google SRE: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/)
- [Google SRE: Service Best Practices](https://sre.google/sre-book/service-best-practices/)
- [Google SRE: Launch Coordination Checklist](https://sre.google/sre-book/launch-checklist/)
