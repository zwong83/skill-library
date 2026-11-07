# Tracing Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Each span answers a latency, failure, causality, or ownership question.
- Auto-instrumented operations are not redundantly wrapped.
- Names are stable and low-cardinality; instance values are attributes.
- Parent/child and link topology matches actual causality, retries, batches, and async work.
- Context is extracted/injected correctly and cannot leak between operations.
- Incoming trace/baggage data is not trusted as security or business state.
- Every span ends exactly once on all paths.
- Attributes follow semantic conventions and are bounded, safe, and useful.
- Status/error behavior matches the operation contract; expected rejections are not mislabeled.
- Logs/events correlate with the active trace without duplicating sensitive payloads.
- Sampling, retention, exporter failure, queue/drop behavior, overhead, and cost are defined.
- Tests verify topology, propagation, status, error, timeout, cancellation, and completion.
