# RabbitMQ Guidance

Apply only when RabbitMQ and its deployed server/client versions are selected.

- Define exchange type, exchange, queue, binding/routing key, durability, queue type, exclusivity/auto-delete, consumer ownership, and topology declaration/change strategy.
- Reliable publishers use publisher confirms and handle unroutable mandatory returns where loss is unacceptable. Publisher confirms and consumer acknowledgements are independent mechanisms; one does not prove the other. See [RabbitMQ Consumer Acknowledgements and Publisher Confirms](https://www.rabbitmq.com/docs/confirms).
- Use manual consumer acknowledgement when processing success must precede deletion. Acknowledge on the same channel according to client rules and only after durable required effects complete.
- Set prefetch from processing concurrency, payload size, latency, memory, and fairness; do not copy a universal value.
- Define `ack`, `nack/reject + requeue`, delayed retry, and dead-letter behavior. Avoid immediate requeue loops.
- Prefer policies for mutable dead-letter configuration where supported. Understand that default dead-letter republishing may not be lossless; RabbitMQ documents stronger at-least-once dead lettering for quorum queues and relevant constraints in [Dead Letter Exchanges](https://www.rabbitmq.com/docs/dlx).
- Evaluate quorum queues, replication, persistence, confirms, and failure behavior against the required durability and availability rather than assuming durable declarations alone prevent loss.
- Monitor publish confirms/returns, ready/unacknowledged counts, consumer capacity, redeliveries, connection/channel churn, memory/disk alarms, queue growth, and DLX failures.
