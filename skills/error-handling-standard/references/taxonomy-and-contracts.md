# Error Taxonomy and Contracts

Use project-specific names, but keep these distinctions when applicable:

| Category | Typical meaning | Retry default |
|---|---|---|
| Validation | Input shape or value is invalid | No; caller corrects input |
| Authentication | Identity is missing or invalid | No; re-authentication may be required |
| Authorization | Identity lacks permission | No |
| Not found | Requested owned resource does not exist or is not visible | No |
| Business rejection | Valid request violates a business rule or state transition | No unless state can legitimately change |
| Conflict/concurrency | Version, uniqueness, idempotency, or concurrent update conflict | Conditional and bounded |
| Rate/resource limit | Quota, throttling, or capacity guard rejected work | Conditional with server guidance |
| Dependency timeout | A dependency exceeded the allocated deadline | Conditional within remaining budget |
| Dependency unavailable | Dependency cannot currently serve the operation | Conditional |
| Cancellation/deadline | Caller cancelled or end-to-end deadline expired | No hidden retry after cancellation |
| Internal defect | Invariant violation or unexpected implementation failure | No automatic retry unless proven transient |

Every public error contract should define a stable code, safe human summary, category, retryability or retry guidance, correlation identifier where appropriate, and field-level validation details when safe. Internal diagnostics remain in protected telemetry.

For HTTP APIs, use the platform's established error envelope. When RFC 9457 Problem Details is selected, define stable `type`, `status`, `title`, and safe extensions without exposing internals. See [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457.html).

Do not infer authorization outcomes from diagnostic identifiers or expose resource existence when policy requires non-disclosure.
