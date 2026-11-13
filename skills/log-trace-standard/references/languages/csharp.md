# C#

Reuse `Microsoft.Extensions.Logging` and the configured provider such as Serilog. Use scopes, `Activity`, and OpenTelemetry integrations for context; verify scope disposal and async flow. Use message templates rather than interpolated strings for structured fields, and configure redaction, providers, and level filters centrally.

## Concrete example

```csharp
logger.LogInformation("【Payment/Create】 Payment created {PaymentId}", paymentId);
```
