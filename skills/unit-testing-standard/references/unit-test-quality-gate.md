# Unit Test Quality Gate

Report each item as `Pass`, `Gap`, or `Not Applicable`:

- Tests trace to a requirement, TA/OpenSpec scenario, defect, or explicit regression risk.
- Assertions prove observable behavior and forbidden effects, not incidental private structure.
- Every TA-assigned behavior has positive coverage; negative and exact boundary partitions plus state, error, duplicate, concurrency, cleanup, and forbidden-effect cases are covered where applicable or have an explicit disposition.
- Time, randomness, global state, and scheduling are controlled.
- Doubles represent stable boundaries and have clear rationale.
- Tests are independent, repeatable, order-insensitive, and free of arbitrary sleeps.
- Failure output identifies the broken behavior.
- Parameterized/property-based cases remain diagnosable.
- Focused and required broader suites were executed with exact results.
- Skips, retries, flaky behavior, limitations, and residual risks are visible.
