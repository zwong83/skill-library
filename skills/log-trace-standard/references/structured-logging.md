# Structured logging

Production events should be machine-readable. A useful baseline is:

```json
{"timestamp":"2026-10-04T15:30:21.123Z","level":"ERROR","service":"payment-service","event":"payment.failed","message":"【Payment/Create】 Payment failed","trace_id":"...","payment_id":"P123","error_code":"PAYMENT_TIMEOUT"}
```

Use consistent keys for timestamp, level, service, event, context IDs, duration, outcome, and domain identifiers. Keep timestamps unambiguous and machine-sortable. Do not serialize whole request/response bodies by default; allow bounded, explicitly redacted diagnostic fields when justified.

## Concrete example

```json
{"timestamp":"2026-10-05T08:10:00Z","level":"INFO","service":"orders","event":"order.created","message":"【Orders/Create】 Order created","trace_id":"abc123","order_id":"O42","duration_ms":87}
```
