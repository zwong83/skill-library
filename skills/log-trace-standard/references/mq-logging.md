# Message-queue logging

Producer logs should identify the event/message type, destination, outcome, bounded message/workflow ID, and trace context. Consumer logs should identify receipt, processing outcome, retry/dead-letter decision, duration, and relevant identifiers. Restore context before processing and clear it afterward.

Never log full message payloads by default. Treat queue contents as untrusted sensitive data and define redaction/retention rules separately from ordinary application logs.

## Concrete example

```text
INFO 【Payments/Consume】 Message processed type=PaymentAuthorized queue=payments message_id=M9 outcome=success duration_ms=31 trace_id=T1
```
