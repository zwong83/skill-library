---
name: backend-messaging-standard
description: Design, implement, or review language-neutral asynchronous messaging and event streaming, including contracts, ownership, delivery semantics, idempotency, ordering, retries, dead letters, outbox/inbox coordination, security, observability, and RabbitMQ, RocketMQ, or Kafka-specific decisions.
---

# Backend Messaging Standard

Use this skill to define reliable asynchronous boundaries. Start with business semantics and failure behavior; select or configure a broker only after those requirements are explicit.

## Core rules

- Define message purpose, producer owner, consumer responsibilities, authoritative data, and compatibility policy before topic/queue names.
- Assume duplicates, delay, redelivery, partial failure, consumer restart, and out-of-order arrival unless a verified broker contract and application design provide stronger scoped guarantees.
- Consumers must be idempotent or safely deduplicate side effects before acknowledging success.
- Acknowledge/commit only after required durable effects complete. Define behavior for partial batch success.
- Do not claim end-to-end exactly-once processing because a producer setting is enabled. State the exact boundary covered and how external side effects and offsets/acknowledgements are coordinated.
- Assign retry ownership, classify retryable failures, bound attempts/backoff, and define dead-letter/quarantine inspection, replay, retention, and ownership.
- Use an ordering/partition/message-group key only for a real invariant; document its scope and throughput consequence.
- Version schemas compatibly and treat message contracts as shared APIs. Never publish framework entities, database rows, or unrestricted internal objects as contracts.
- Propagate trace context safely and design structured producer/consumer events without using correlation metadata for authorization.
- Do not introduce RabbitMQ, RocketMQ, Kafka, or multiple brokers without requirements and trade-offs that justify them.

## Workflow

1. Classify command, event, notification, stream record, request/reply, scheduled/delayed message, or integration transfer.
2. Define producer/consumer ownership, contract, authority, privacy, compatibility, and lifecycle.
3. Choose delivery, durability, ordering, replay, latency, throughput, retention, and availability requirements.
4. Design publish coordination, consumer transaction/idempotency, acknowledgement/offset, retry, dead-letter, and recovery behavior.
5. Select broker and map the technology-neutral contract to its verified semantics and deployed version.
6. Define topology, capacity, quotas, security, observability, rollout, migration, and operational ownership.
7. Test duplicates, loss windows, redelivery, reordering, poison messages, partial batches, rebalance/failover, schema evolution, and replay.

## Readiness gate

Require message purpose, producer owner, known consumer responsibilities, authoritative state, delivery/durability/ordering/replay requirements, failure ownership, data classification, and operational ownership. For SDD, require the approved broker/topology decision and deployed broker/client versions. Block implementation-ready status when contract ownership, publish consistency, acknowledgement point, idempotency, retry/DLQ behavior, or compatibility policy is unresolved.

## Reference routing

- Read [references/contracts-and-compatibility.md](references/contracts-and-compatibility.md) for envelopes, schemas, versioning, ownership, privacy, and trace context.
- Read [references/delivery-idempotency-and-recovery.md](references/delivery-idempotency-and-recovery.md) for publish coordination, acknowledgement, offsets, retries, ordering, dead letters, and replay.
- Read only the selected broker reference: [RabbitMQ](references/rabbitmq.md), [RocketMQ](references/rocketmq.md), or [Kafka](references/kafka.md).
- Read [references/review-checklist.md](references/review-checklist.md) before approval.

## SD and SDD boundary

System Design defines interaction style, broker decision, ownership, topology, contract/versioning strategy, delivery and ordering guarantees, publish/consume consistency, retry/DLQ/replay, security, capacity, and operations. SDD/OpenSpec defines concrete topics/exchanges/queues/groups, schemas, keys, adapters, handlers, transaction/ack code paths, configuration, migration tasks, and tests.

## Companion skills

Invoke `backend-error-handling-standard` for failure taxonomy and boundary behavior, `logging-standard` for operational/audit events, `tracing-standard` for producer/consumer propagation and links, and `backend-caching-standard` only when messaging drives cache invalidation or materialization.

## Expected output

Provide a messaging decision record, ownership/topology map, contract and compatibility rules, delivery/ordering/idempotency model, publish/consume sequence, retry/DLQ/replay plan, broker-specific settings with version assumptions, security and observability plan, capacity model, rollout/migration strategy, and verification evidence.
