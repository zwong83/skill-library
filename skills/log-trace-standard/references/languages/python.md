# Python

Use the standard `logging` ecosystem or the project's established `structlog` setup. Use `contextvars` or framework middleware for request/trace context and configure handlers centrally. Prefer lazy logger arguments, structured formatters, bounded exception data, and OpenTelemetry integration where present. Avoid configuring the root logger inside reusable libraries.

## Concrete example

```python
logger.info("【Payment/Create】 Payment created", extra={"event": "payment.created", "payment_id": payment_id, "trace_id": trace_id})
```
