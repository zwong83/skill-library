---
name: backend-performance-capacity-standard
description: Design, implement, or review measurable software performance and capacity, including workload models, latency and throughput objectives, resource budgets, bottlenecks, queues, saturation, scalability, load testing, headroom, dependency quotas, autoscaling, forecasting, and performance regression evidence.
---

# Backend Performance and Capacity Standard

Use this skill when response time, throughput, concurrency, resource use, growth, scalability, or launch capacity can affect product or operational success.

## Core Rules

1. Translate product journeys and SLOs into measurable latency, throughput, concurrency, error, freshness, and resource objectives. Avoid “fast” or “high scale.”
2. Model representative workload shape, mix, data size, arrival pattern, locality, growth, and peak behavior before selecting optimizations or infrastructure.
3. Use percentiles and distributions for latency; averages may hide tail behavior.
4. Measure before optimizing. Identify the limiting resource and preserve correctness, security, and maintainability.
5. Bound queues and concurrency. Include queueing time and downstream time in end-to-end budgets.
6. Distinguish load, stress, spike, soak, scalability, and component benchmark evidence. One test cannot answer every question.
7. Include dependencies, quotas, connection pools, cache behavior, storage growth, autoscaling lag, startup time, and failover capacity.
8. Maintain explicit headroom for traffic variation, deployment, failover, maintenance, and forecast error.
9. Compare like-for-like baselines and control test environment, dataset, tooling, warm-up, duration, and noise.
10. Make performance regressions observable and assign capacity thresholds and ownership.

## Workflow

1. Identify critical journeys, SLOs, deadlines, business peaks, growth, and failure consequences.
2. Build a workload and data model with traffic mix, concurrency, arrival pattern, locality, payloads, and dependency calls.
3. Allocate end-to-end latency and resource budgets across components.
4. Establish a reproducible baseline and instrument latency, throughput, errors, queues, saturation, and resources.
5. Find bottlenecks through measurement and test the smallest justified change.
6. Model capacity, headroom, scaling triggers, quotas, failover, and forecast horizons.
7. Run the appropriate benchmark/load/stress/spike/soak/scalability tests and analyze confidence and limitations.
8. Define release gates, production guardrails, regression detection, and capacity review cadence.

## Readiness Gate

Performance and capacity design is ready only when:

- critical journeys have measurable objectives and percentile definitions;
- workload, data, growth, peak, and dependency assumptions are explicit;
- latency and resource budgets are allocated end to end;
- queue, concurrency, timeout, pool, quota, and saturation behavior is defined;
- baseline and test environments are reproducible enough for the decision;
- headroom covers rollout, failover, maintenance, and forecast error;
- scaling signals, limits, lag, and fallback are defined;
- regression gates, monitoring, ownership, and review cadence exist;
- unresolved target or capacity assumptions block affected approval.

## Reference Routing

- Read [objectives-workloads-and-budgets.md](references/objectives-workloads-and-budgets.md) for target definitions, workload models, latency decomposition, queues, and resource budgets.
- Read [testing-capacity-and-regression.md](references/testing-capacity-and-regression.md) for performance test types, capacity/headroom, forecasting, autoscaling, and evidence.
- Invoke `backend-resilience-standard` for overload, backpressure, deadlines, retries, degradation, and failover.
- Invoke `db-standard`, `cache-standard`, or `message-standard` for technology-specific bottlenecks and capacity behavior.
- Invoke `backend-operability-standard` for production indicators, dashboards, thresholds, alerts, and runbooks.
- Invoke `testing-strategy-standard` to place performance tests in the overall risk-based test portfolio.

## System Design and SDD Boundary

- In System Design, decide objectives, workload assumptions, budgets, capacity model, headroom, scaling approach, and required evidence.
- In SDD, implement approved instrumentation, bounds, configuration, optimizations, test harnesses, datasets, gates, dashboards, and evidence.
- Return material target, workload, topology, datastore, consistency, or scaling changes to System Design.

## Expected Output

Return objectives and definitions, workload/data model, latency and resource budgets, baseline, bottleneck evidence, capacity/headroom and scaling plan, test plan/results, regression gates, production guardrails, assumptions, risks, and unresolved decisions.
