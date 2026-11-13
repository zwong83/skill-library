# Exception logging

At the boundary that owns a failure, record the event, operation, stable error code/category, safe identifiers, context IDs, and the original exception with stack trace. Preserve causal chains and avoid replacing useful exceptions with generic text.

Handle expected business outcomes without stack traces when they are not faults. Avoid logging and rethrowing the same exception at every layer; lower layers may add context and rethrow, while the owning boundary emits the final error event.

## Concrete example

```text
ERROR 【Payment/Create】 Payment failed payment_id=P123 error_code=PAYMENT_TIMEOUT exception=TimeoutError trace_id=T1
```
