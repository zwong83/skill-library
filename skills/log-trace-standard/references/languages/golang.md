# Go

Prefer the project's `log/slog`, zap, or zerolog ecosystem. Pass `context.Context` through boundaries and derive logger fields from it; do not use a global mutable request context. Use structured attributes, error wrapping with `%w`, and bounded asynchronous sinks where justified. Check shutdown flushing and behavior under backpressure.

## Concrete example

```go
slog.InfoContext(ctx, "【Payment/Create】 Payment created", "event", "payment.created", "payment_id", paymentID)
```
