# Error Codes and Default Messages

## Define and reuse the pair

1. Check the owning domain's enum and the shared application enum for the same failure. Reuse an existing member when its meaning matches.
2. If the failure is distinct, add one enum member with an explicit integer `code` and a non-empty text `message`. Allocate a unique code within the published error namespace and keep it stable. Write the message so callers can safely see it without request-specific data.
3. Pass the enum member to exception constructors, factories, and typed error results. A reusable exception class for one failure can bind its member internally. Derive the exception message from the enum and store instance context and original causes separately.
4. Serialize the numeric `code` and text `message` from the same member. Assign application codes independently of HTTP status, vendor codes, and enum declaration order. Map protocol status, retry, or acknowledgement behavior at the boundary. If disclosure policy requires a different public outcome, use the enum member for that outcome.
5. Verify that all paths for the same failure emit the same pair. Review compatibility before changing a published code, its type, or its default message. If an existing public contract uses string codes, plan an explicit migration or versioned mapping.

## Illustrative code catalog

| Enum member | Numeric `code` | Text `message` | Typical use |
|---|---|---|---|
| `ACCOUNT_LOCKED` | `1001` | Account is locked. | The account lock rule rejects an operation. |
| `INVALID_INPUT` | `1002` | One or more inputs are invalid. | A validation failure with optional field details kept separately. |
| `INTERNAL_ERROR` | `9000` | An unexpected error occurred. | An unmapped failure whose cause stays in protected diagnostics. |

Use the project's approved meanings and published values when adopting this structure.

## Language-neutral definition

```text
enum ErrorCode with fields (code: integer, message: text)
    ACCOUNT_LOCKED = (1001, "Account is locked.")
    INVALID_INPUT  = (1002, "One or more inputs are invalid.")
    INTERNAL_ERROR = (9000, "An unexpected error occurred.")
```

The exception takes its message from the member's `message`. A typed error result retains the same member. Both paths produce the same fields at the boundary.

```json
{
  "code": 1001,
  "message": "Account is locked."
}
```

See [Exception Engineering Examples](examples.md) for language-neutral exception and handler examples.
