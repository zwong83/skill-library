# Observability boundaries

Logs, metrics, and traces complement one another. Use logs for meaningful event detail, metrics for aggregate rates and thresholds, and traces for end-to-end timing and topology. Link them with shared service and trace identifiers, but do not duplicate every metric or span as a log. Use a dedicated audit/event mechanism when immutable business history is required.

## Concrete example

For a slow checkout, a metric shows elevated latency, a trace identifies the payment span, and one structured log explains `payment.provider_timeout` with the safe payment ID and error code.
