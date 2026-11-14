# Comment Types

## Intent and rationale

Explain why the chosen approach exists, what alternative was rejected, and which requirement or constraint makes the choice necessary. Keep architectural history in an ADR/SDD and link to it when needed.

## Invariants and contracts

Document rules not enforced by types or structure: valid states, units, ranges, ownership, ordering, idempotency, nullability, mutation, compatibility, and error behavior.

## Concurrency and lifecycle

Explain lock ordering, thread/task ownership, atomicity, visibility, cancellation, cleanup, resource lifetime, callback reentrancy, and shutdown assumptions. A comment does not replace synchronization or tests.

## Security and privacy

Explain trust boundaries, sanitization requirements, constant-time or fail-closed constraints, redaction, and why a check must not be removed. Do not disclose secrets, exploit details that violate policy, or sensitive production information.

## Algorithms and formats

Explain the mathematical idea, complexity trade-off, approximation, protocol quirk, bit layout, regex intent, encoding, units, or external specification. Prefer a stable source link and test cases for edge conditions.

## Workarounds

State the external defect/limitation, affected versions or condition, safe removal trigger, and stable reference. Avoid indefinite “temporary” comments.

## TODO and FIXME

Use only for acknowledged incomplete work. State the required outcome and why it cannot be completed now, plus an issue/owner/trigger according to project convention. Never use TODO to conceal a requirement or test needed for the current task.
