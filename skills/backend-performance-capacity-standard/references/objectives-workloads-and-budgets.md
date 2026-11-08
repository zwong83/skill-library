# Objectives, Workloads, and Budgets

## Objective Contract

For each critical journey define:

- measurement boundary and user or caller population;
- latency percentile and window, including timeout/cancelled treatment;
- throughput and concurrency range;
- acceptable error, rejection, freshness, and correctness behavior;
- payload/data-size range and cache state;
- normal, peak, degraded, and recovery targets;
- geographic or network assumptions;
- source requirement, owner, and approval status.

Do not compare percentiles computed with different windows, populations, or excluded failures.

## Workload Model

Capture request or job mix, arrival distribution, burst length, concurrency, think time, read/write ratio, key locality, tenant skew, payload sizes, dataset cardinality, background work, scheduled peaks, retries, and dependency fan-out. Include expected growth and exceptional launch or seasonal events.

Closed-loop virtual-user tests and open-loop arrival tests answer different questions. Choose the model that reflects production demand and disclose coordinated-omission or client-saturation risk.

## End-to-End Budget

Decompose the caller deadline into queueing, application work, network, dependency, storage, serialization, and response time. Preserve cleanup margin and propagate the remaining budget. Avoid assigning every component the full end-to-end deadline.

Track at least:

- request/job rate and completion rate;
- latency distributions by meaningful bounded dimensions;
- errors, timeouts, cancellations, retries, and rejections;
- active work, queue depth/wait, pool wait, and saturation;
- CPU, memory, allocation/GC, threads/processes, network, disk, and dependency quotas as applicable.

## Bottleneck Reasoning

Change one material variable at a time when feasible. Correlate throughput and latency with saturation. A faster component does not improve end-to-end performance if another resource remains limiting. Re-test correctness and tail behavior after every optimization.

Use language/runtime profilers and datastore plans appropriate to the stack. Do not infer a production bottleneck from a microbenchmark alone.
