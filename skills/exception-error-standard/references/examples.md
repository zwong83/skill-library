# Exception Engineering Examples

These examples use pseudocode. Apply the same contract using the project's language and framework conventions.

## Reuse a domain exception type

Define the code and default message together in the [error-code enum](error-codes-and-messages.md). If the project has a `DomainException` base class that accepts the enum type, bind the exception to its member. The base class sets its message from that member.

```text
exception AccountLockedException extends DomainException
    initialize with ErrorCode.ACCOUNT_LOCKED
```

Both sign-in and account update can throw a fresh `AccountLockedException` when they encounter the same lock rule. A use case that returns a typed error for the same rule also uses `ErrorCode.ACCOUNT_LOCKED`. The boundary maps the member to a response with its explicit code and default message.

## 1. Assertion: condition to application exception

An assertion owns the condition check and the failure path. It should not perform database access, logging, response formatting, or exception translation.

```text
function requirePresent(value, error):
    if value is null:
        throw ExceptionFactory.business(error)

requirePresent(user, ErrorCode.USER_NOT_FOUND)
```

Use an assertion when the caller wants a compact guard clause. Use a normal `if` when the failure needs substantial local logic or several pieces of context.

## 2. Factory: create without throwing

A factory returns an exception object. The caller remains responsible for deciding whether and where to throw it.

```text
exception = ExceptionFactory.business(ErrorCode.ACCOUNT_LOCKED)
throw exception
```

Prefer a factory when the exception needs additional context, when a caller may aggregate errors, or when tests need to inspect the created exception before throwing.

## 3. Translator: infrastructure exception to domain exception

Translation belongs close to the integration boundary or in a dedicated translator. Preserve the original cause and avoid exposing vendor-specific details to higher layers.

```text
try:
    repository.save(entity)
catch databaseFailure as cause:
    throw ExceptionTranslator.database(cause)
```

```text
Socket timeout          -> ExternalServiceTimeoutException
UniqueConstraintError   -> ResourceAlreadyExistsException
Database driver failure -> DatabaseAccessException
VendorApiError(401)     -> ExternalServiceAuthenticationException
```

Do not translate an exception merely to change its class name. The new exception should add domain meaning, stable error semantics, or an appropriate recovery category.

## 4. Boundary handler: exception to response or action

Handlers belong at application boundaries and should map stable application errors to protocol-specific output.

```text
function handleBusinessFailure(exception):
    error = exception.errorCodeMember
    status = mapHttpStatus(error)
    return response(status, body = {code: error.code, message: error.message})
```

```text
BusinessException      -> HTTP 4xx response
ValidationException    -> field-level validation response
MessageProcessingError -> retry, reject, or dead-letter decision
UnexpectedException    -> generic response plus server-side diagnostic
```

Keep protocol details out of domain exceptions. A domain exception should not need to know about HTTP status codes, message acknowledgements, or UI response shapes.

## 5. Naming migration map

First inspect what each old class actually does; then split mixed classes where needed.

| Existing name | Actual behavior | Preferred destination |
|---|---|---|
| `AssertUtil.notNull` | Checks and throws | `ExceptionAssert.notNull` |
| `ExceptionUtil.business` | Returns exception | `ExceptionFactory.business` |
| `ExceptionUtil.throwBusiness` | Throws exception | `ExceptionThrower.throwBusiness` or an explicit `throw ExceptionFactory.business(...)` |
| `ExceptionMapper.database` | Wraps infrastructure error | `ExceptionTranslator.database` |
| `ExceptionMapper.toResponse` | Converts exception to HTTP/MQ output | Boundary-specific `ExceptionHandler` |

If one old utility contains several rows of behavior, do not rename the file and leave the mixed responsibilities intact. Extract cohesive components and migrate callers by responsibility.

## 6. Anti-patterns

- A catch-all helper that asserts, translates, logs, and formats HTTP responses.
- A translator that discards the original cause.
- A domain exception that accepts an inline string code, custom default message, HTTP status, or route.

Prefer small, cohesive operations with a stable exception type, error code, cause chain, and context policy. Add aliases or adapters only when backward compatibility is required.

## 7. Review checklist

- Does the name describe what the code does rather than merely calling it a utility?
- Does the method clearly return an exception or throw one?
- Is translation adding domain meaning and preserving the cause?
- Is response, retry, acknowledgement, or logging policy kept at the boundary?
- Are numeric codes, default messages, and exception types stable for callers?
- Are tests covering success, failure, cause preservation, and boundary mapping?
