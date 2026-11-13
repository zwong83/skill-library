# Rust

Prefer the project's `tracing` and `tracing-subscriber` ecosystem. Use spans and entered scopes for context, attach structured fields, and integrate OpenTelemetry when required. Preserve error sources with the project's error conventions. Verify subscriber filtering, async span propagation, and shutdown flushing.

## Concrete example

```rust
tracing::info!(event = "payment.created", payment_id = %payment_id, "【Payment/Create】 Payment created");
```
