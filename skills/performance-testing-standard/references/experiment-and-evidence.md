# Performance experiments and evidence

## Experiment selection

Select from the question and approved acceptance criteria; these are alternatives or complementary experiments, not a mandatory suite.

| Experiment | Question and evidence |
|---|---|
| Benchmark | Cost/latency of a defined operation under controlled conditions; report setup, warm-up, repetitions and variation. |
| Load | Does the approved workload meet its latency/throughput/error objectives over the required window? Record offered and achieved work. |
| Stress | Where does a bounded increasing workload breach criteria, and how does the system fail/recover? Do not exceed authorized limits to find a breaking point. |
| Spike | Can the system absorb an approved abrupt change and recover? Capture the transition, queueing/errors and recovery timeline. |
| Soak | Does sustained work reveal memory/resource growth, leaks, backlog or degradation over the required duration? A short run cannot substitute. |
| Scalability/capacity | What measured configuration and workload satisfy all constraints, with justified headroom? Compare controlled configurations; do not extrapolate linearly without evidence. |
| Failover capacity | Does the approved degraded topology sustain its assigned workload and recovery requirements? Inject faults only within separately explicit fault/target authorization. |
| Performance regression | Does the target revision meet absolute criteria and the accepted change tolerance against a comparable baseline? Account for environment drift and variation. |

## Workload and validity

Model sessions, request sequences, authentication, think time, payload and key distributions and read/write/tenant mix where they affect the question. Declare whether arrival is independent of completion or concurrency is bounded by user behavior. A closed model slows new iterations when responses slow; an open model schedules arrivals independently. Match this distinction to the intended traffic rather than choosing whichever produces a better result. See [Grafana k6 open and closed models](https://grafana.com/docs/k6/latest/using-k6/scenarios/concepts/open-vs-closed/) for a concrete tool implementation.

Count unscheduled or dropped work explicitly and investigate its cause. In k6, dropped iterations can reflect executor allocation/configuration or target slowdown; a drop alone does not isolate the cause. Correlate generator headroom and target evidence and do not silently discard those iterations from workload sufficiency. See [Grafana k6 dropped iterations](https://grafana.com/docs/k6/latest/using-k6/scenarios/concepts/dropped-iterations/).

Translate approved criteria into automated pass/fail checks where possible, keeping safety aborts distinct from acceptance. In k6, metric thresholds can make a test fail when the specified conditions are not met. Example documentation values are not project SLOs. See [Grafana k6 thresholds](https://grafana.com/docs/k6/latest/using-k6/thresholds/). These references illustrate semantics; they do not mandate k6 or authorize its installation.

Compare distributions from equivalent populations, not just averages or one favorable percentile. Retain sample counts and failure/time-out treatment, warm-up exclusion rules, data/cache state, repetitions and variation. Keep original histograms/samples when available; averaging reported percentiles is not a substitute for computing a combined distribution. Separate time-series phases and preserve outliers unless an established rule justifies exclusion. Diagnose target and generator bottlenecks independently and disclose environmental differences.

## Compact evidence record

| Field | Required content when applicable |
|---|---|
| Identity | Source/approved source/test case IDs, experiment, baseline/target revisions, timestamps and owner |
| Workload | Model, mix/data distribution, planned rate/concurrency, achieved work, phases, duration and repetitions |
| Conditions | Target/dependency/tool/generator versions and topology, quotas, cache state, warm-up and measurement settings |
| Criteria | Approved metric populations/windows/thresholds, correctness checks, comparison tolerance and abort limits |
| Authorization | Target/environment/load/fault scope reference, stop owner and data/evidence handling |
| Results | Actual commands/configuration, raw artifacts, distributions/time series, errors/timeouts/drops, resource/queue evidence |
| Recovery | Abort reason, backlog/health/integrity checks, cleanup and restoration status |
| Interpretation | Validity, uncertainty, comparability, bounded bottleneck hypotheses and scope of capacity claims |
| Handoff | Case and overall verdicts, numbered workflow outcomes, unrun checks, gaps, next owners and residual risk |

Existing CI/test reports can supply these fields; do not duplicate an evidence store solely to satisfy a filename. Redact credentials and private payloads while retaining reproducible configuration references.
