# Logging requirements

## Scope
- Services/components:
- Environments:
- Deployment model:

## Events and context
- Required event categories:
- Required fields:
- Message prefix format, if required (for example, `【Service/Operation】`):
- Trace/request propagation:

## Operations
- Output and collector:
- Levels and sampling:
- Rotation/retention:
- Volume and latency limits:

## Security
- Prohibited fields:
- Redaction strategy:
- Access and retention policy:

## Concrete example

For `payment-service`, require `payment.created` and `payment.failed`, propagate W3C trace context, write JSON to stdout in production, and retain redacted logs for 30 days.
