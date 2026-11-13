# RocketMQ Guidance

Apply only when Apache RocketMQ and its deployed broker/client versions are selected.

## Version and architecture gate

- Record RocketMQ broker, Proxy, client/SDK, protocol, and console/admin-tool versions before selecting APIs or configuration. Separate 4.x guidance from the 5.x message model, Proxy, SDK, topic message-type validation, and HA capabilities.
- Define NameServer, Broker, Proxy where applicable, producer/consumer placement, network zones, failure domains, discovery path, and ownership. The RocketMQ 5.x deployment documentation describes NameServer, Broker, and Proxy roles: [Deployment method](https://rocketmq.apache.org/docs/deploymentOperations/01deploy/).
- Define topic, enforced message type where supported, queue count, producer and consumer groups, clustering/broadcast consumption, subscription/filter consistency, message key/tag, retention, permissions, and change process.
- Do not treat a message offset, message ID, send result, or broker persistence as proof that downstream business processing completed.

## Producer design

- Select synchronous, asynchronous, one-way, or batch send from business durability, latency, throughput, callback, and loss tolerance. One-way sending is not a default for important business events.
- Define producer lifecycle/reuse, thread safety, route refresh, queue selection, payload/attribute limits, serialization, compression if applicable, timeout, send retry, throttling, and graceful shutdown.
- Treat timeout or lost acknowledgement as an uncertain outcome: the broker may or may not have accepted the message. Use stable message/business identity, idempotent consumers, and reconciliation rather than blindly assuming failure or success.
- Coordinate the local database transaction and message publication through a verified mechanism such as RocketMQ transactional messages, transactional outbox/CDC, or explicit reconciliation. A normal database commit plus send is not atomic.

## Consumer design

- Select PushConsumer or SimpleConsumer from control, throughput, batching, and processing-time requirements. Define lifecycle, subscription, concurrency, queue allocation, rebalance behavior, processing/invisibility timeout, and downstream resource limits.
- Define the exact success/commit point. Complete required durable business effects and idempotency recording before returning success or acknowledging completion.
- Consumers remain idempotent because producer uncertainty, timeout, restart, retry, and recovery can redeliver work. Prefer atomic business update plus dedup/inbox state where the datastore supports it.
- RocketMQ retries failed or timed-out consumption and moves messages to DLQ after configured retry exhaustion; behavior varies by consumer type. Define interval, maximum retries, age, ordered-message impact, DLQ owner, alert, retention, inspection, correction, replay, and reconciliation. See [Consumption Retry](https://rocketmq.apache.org/docs/featureBehavior/10consumerretrypolicy/).
- For backlog recovery, model production rate, current lag/age, consumer service rate, downstream capacity, drain time, and throttled scale-up. Do not overload the database while draining the broker.

## Message types and contracts

- Match normal, FIFO, delayed, or transactional messages to an explicit requirement; do not select advanced types by default. Starting with RocketMQ 5.0, topic/message-type compatibility is part of the design; verify the deployed version. See [RocketMQ Topic](https://rocketmq.apache.org/docs/domainModel/02topic/).
- For FIFO, define the business message group, producer serialization, consumer receive-process-reply ordering, retry blocking, and throughput trade-off. Ordering applies within a message group, not globally across groups. See [Ordered Message](https://rocketmq.apache.org/docs/featureBehavior/03fifomessage/).
- For delayed messages, define target delivery timestamp, timezone/clock assumptions, maximum supported delay, expiry, duplicate/late delivery, cancellation, and version-specific limits. See [Delay Message](https://rocketmq.apache.org/docs/featureBehavior/02delaymessage/).
- For transactional messages, define half-message send, local transaction execution, commit/rollback, transaction-check handler, unknown status, check idempotency, maximum check behavior, and reconciliation. This provides a scoped eventual-consistency mechanism, not an end-to-end exactly-once business transaction. See [Transaction Message](https://rocketmq.apache.org/docs/featureBehavior/04transactionmessage/).
- For tag or attribute filtering, define ownership, compatibility, unmatched-message behavior, and broker/client version support. See [Message Filtering](https://rocketmq.apache.org/docs/featureBehavior/07messagefilter/).
- Bound batch count and bytes. Define partial construction/send/consume behavior and use external object storage references for oversized payloads only with access, lifecycle, integrity, and cleanup rules.

## Reliability and infrastructure

- Define persistence/flush, replication, acknowledgement, failure, and recovery requirements against explicit RPO/RTO. Do not infer zero loss from a generic “send success” statement.
- Select and document the deployed HA topology, automatic failover mechanism, write availability during failure, replica synchronization, metadata/controller dependencies where applicable, maintenance behavior, and cross-region strategy. Verify with failure tests for that exact topology.
- Capacity planning must cover messages/second, average/peak payload, daily volume, retention, replication/storage overhead, queue count, producer concurrency, consumer throughput, backlog headroom, disk I/O, memory/page cache, CPU, network, and downstream pools.
- Treat multi-tenant topic/group boundaries, ACLs, quotas, noisy-neighbor isolation, data residency, retention/deletion, and cost ownership as explicit decisions.

## Operations and verification

- Monitor producer send latency/failures/uncertain results, broker/store/replication health, disk and page-cache pressure, topic/queue distribution, consumer throughput, lag/backlog age, inflight timeout, retries, DLQ, rebalances, ordered-message blocking, and replay progress.
- Define runbooks for unavailable NameServer/Proxy/Broker, disk pressure, route/subscription errors, missing/duplicate messages, backlog, retry storms, DLQ recovery, offset reset/replay, rolling upgrade, rollback, and regional failure.
- Test with a real compatible broker/client combination: duplicate delivery, producer timeout ambiguity, consumer crash before/after business commit, retry exhaustion, ordered-message blocking, transactional check/recovery, schema evolution, broker failover, network delay/partition, disk pressure in an isolated environment, backlog drain, upgrade, and rollback.
- Benchmark with realistic payloads and concurrency. Measure throughput plus p50/p95/p99/max latency, resource saturation, backlog growth/drain, and behavior during failure; do not tune from average latency alone.
