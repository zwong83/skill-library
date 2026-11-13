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

Every public error contract should use the enum's stable integer `code` and safe text `message`. Define the category, retryability or retry guidance, correlation identifier where appropriate, and field-level validation details when safe. Internal diagnostics remain in protected telemetry.

## Error-code enum

- Declare one member per distinct application failure in the enum owned by the domain or shared contract. Each member defines the code and default message that exceptions, typed results, and boundary mappings reuse. See [Error codes and default messages](error-codes-and-messages.md) for definitions and examples.
- Give domain exception classes a fixed member when they represent one business failure. Shared exception types and typed results should accept an enum member in their constructor or factory. Keep the public status or protocol action in the boundary mapping.
- Translate known dependency failures to their application members. Route unmapped failures through an internal-error member and retain the original cause in protected diagnostics. Preserve published values during refactoring.

## Domain exception types

Define one reusable exception type in the owning domain for each business failure represented by an exception. Reuse that type across use cases, assertions, factories, and translators when they represent the same failure. Create an instance per occurrence and supply relevant context and any original cause.

Extend an existing domain base exception when it provides the right shared contract. Extend a more specific exception only when callers can handle the subtype under that parent contract and the subtype adds distinct business meaning or handling. Map protocol-specific details at the boundary.

For HTTP APIs, use the platform's established error envelope. When RFC 9457 Problem Details is selected, define stable `type`, `status`, `title`, and safe extensions without exposing internals. See [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457.html).

Do not infer authorization outcomes from diagnostic identifiers or expose resource existence when policy requires non-disclosure.
