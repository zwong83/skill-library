# Retry and Recovery

Retry is a state transition with cost and side effects, not a generic exception handler.

## Retry decision

Require all of the following:

- the failure is classified as transient;
- the operation is idempotent, deduplicated, or otherwise safe to repeat;
- the remaining end-to-end deadline can accommodate another attempt;
- attempts, backoff, jitter, concurrency, and resource consumption are bounded;
- retry ownership is assigned to one layer to prevent multiplicative retry storms;
- exhaustion has an explicit terminal action and observable signal.

Do not retry validation, authorization, stable business rejection, malformed messages, deterministic serialization errors, or known invariant violations.

## Recovery choices

| Mechanism | Use when | Required decision |
|---|---|---|
| Immediate retry | Very short transient fault and low contention | Attempt count and timeout budget |
| Exponential/backoff retry | Dependency recovery needs time | Backoff, jitter, cap, exhaustion |
| Circuit breaker | Repeated calls would amplify dependency failure | Open/half-open policy and fallback |
| Fallback | Degraded result is safe and product-approved | Correctness, staleness, and user visibility |
| Compensation | A completed distributed step must be semantically undone | Idempotency, ordering, and reconciliation |
| Dead letter/quarantine | Work cannot currently be processed safely | Ownership, inspection, replay, retention |
| Manual reconciliation | Automation cannot determine a safe outcome | Evidence, access, SLA, and audit trail |

Timeouts must be derived from an end-to-end budget. A lower layer must not independently retry past the caller's deadline or continue expensive work after cancellation unless the contract explicitly requires detached processing.
