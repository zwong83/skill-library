---
name: message-standard
description: Design, implement, review, or troubleshoot language-neutral asynchronous messaging and event streaming, including contracts, ownership, delivery semantics, idempotency, ordering, retries, dead letters, outbox/inbox coordination, security, observability, and Kafka, RabbitMQ, RocketMQ, and Pulsar.
---

# Messaging Standard

Use this skill to define reliable asynchronous boundaries. Start with business semantics and failure behavior; select or configure a broker only after those requirements are explicit.

## Core rules

- Define message purpose, producer owner, consumer responsibilities, authoritative data, and compatibility policy before topic/queue names.
- Assume duplicates, delay, redelivery, partial failure, consumer restart, and out-of-order arrival unless a verified broker contract and application design provide stronger scoped guarantees.
- Consumers must be idempotent or safely deduplicate side effects before acknowledging success.
- Use at-least-once delivery with idempotent processing as a starting point when loss is unacceptable and the full pipeline cannot prove stronger guarantees.
- Acknowledge/commit only after required durable effects complete. Define behavior for partial batch success.
- Do not claim end-to-end exactly-once processing because a producer setting is enabled. State the exact boundary covered and how external side effects and offsets/acknowledgements are coordinated.
- Assign retry ownership, classify retryable failures, bound attempts/backoff, and define dead-letter/quarantine inspection, replay, retention, and ownership.
- Set a backlog or message-age limit. When input exceeds processing capacity, choose bounded flow control, throttling, batching, scaling, or an explicit shedding policy based on the delivery contract.
- Use an ordering/partition/message-group key only for a real invariant; document its scope and throughput consequence.
- Version schemas compatibly and treat message contracts as shared APIs. Never publish framework entities, database rows, or unrestricted internal objects as contracts.
- Propagate trace context safely and design structured producer/consumer events without using correlation metadata for authorization.
- Do not introduce RabbitMQ, RocketMQ, Kafka, Pulsar, or multiple brokers without requirements and explicit operational rationale.

## Mandatory workflow

**Complete steps 1 through 7 in order for every messaging task.** Identify the task mode and scope first. Carry out each applicable step and record its outcome. For an existing system, confirm applicable decisions against the current contract and evidence. A focused task can make a step brief, but it still needs an outcome. Use `Not applicable` only when a step does not apply and record why. Mark a step `Blocked` when it lacks a required input or decision, and stop dependent work.

Identify the affected lifecycle stages for a focused change or incident. Check producer acceptance, broker capacity, consumer lag or rebalancing, downstream saturation, and acknowledgements as relevant before changing retry limits or concurrency.

1. Classify command, event, notification, stream record, request/reply, scheduled/delayed message, or integration transfer.
2. Define producer/consumer ownership, contract, authority, privacy, compatibility, and lifecycle.
3. Choose delivery, durability, ordering, replay, latency, throughput, retention, and availability requirements.
4. Design publish coordination, consumer transaction/idempotency, acknowledgement/offset, retry, dead-letter, and recovery behavior.
5. Select broker and map the technology-neutral contract to its verified semantics and deployed version.
6. Define topology, capacity, quotas, security, observability, rollout, migration, and operational ownership.
7. Verify the applicable cases for duplicates, loss windows, redelivery, reordering, poison messages, partial batches, rebalance or failover, schema evolution, and replay. Run the relevant checks for implementation, specify them for design, and assess available evidence for review.

## Readiness gate

Require message purpose, producer owner, known consumer responsibilities, authoritative state, delivery/durability/ordering/replay requirements, failure ownership, data classification, and operational ownership. For SDD, require the approved broker/topology decision and deployed broker/client versions. Block implementation-ready status when contract ownership, publish consistency, acknowledgement point, idempotency, retry/DLQ behavior, or compatibility policy is unresolved.

Claim completion only after every workflow step has a recorded outcome. A blocked applicable step prevents a readiness claim. Report planned checks as pending verification until they run.

## Choose references for the task

Start with the reference or section that answers the requirement. Load broker-specific details only when a broker is selected or is a serious candidate. Add another reference only if a separate contract, implementation, or diagnostic question needs it.

| Decision or symptom | Start here |
|---|---|
| Choose queue versus stream, or locate the stage that failed | [Messaging fundamentals](references/messaging-fundamentals.md) |
| Define an envelope, owner, schema, privacy boundary, version, or compatibility policy | [Contracts and compatibility](references/contracts-and-compatibility.md) |
| Choose at-most-once, at-least-once, or a scoped exactly-once guarantee | [Delivery semantics](references/delivery-semantics.md) |
| Avoid a lost publish after a database commit or coordinate an outbox, CDC, or broker transaction | [Publish coordination](references/delivery-idempotency-and-recovery.md#publish-coordination) |
| Prevent a duplicate business effect | [Idempotency](references/idempotency.md). Use [consumer processing](references/delivery-idempotency-and-recovery.md#consumer-processing) when ACK, offset commit, or partial batch behavior also matters. |
| Preserve ordering with concurrent consumers, or define retry, dead letters, and replay | Start with the affected section in [delivery and recovery](references/delivery-idempotency-and-recovery.md). |
| Review a messaging design or its readiness | [Review checklist](references/review-checklist.md) for items in scope |

For a broker-specific task, choose one column for the broker involved. Load both only if troubleshooting requires a design or configuration decision.

| Broker | Design and configuration | Operational symptom |
|---|---|---|
| Kafka | [Partitions, groups, offsets, and transactions](references/kafka.md) | [Lag, rebalances, and broker health](references/kafka-operations.md) |
| RabbitMQ | [Exchanges, queues, confirms, and acknowledgements](references/rabbitmq.md) | [Queue depth, unacked messages, and dead lettering](references/rabbitmq-operations.md) |
| RocketMQ | [Topology, message types, and consumption modes](references/rocketmq.md) | [Lag, retries, DLQ, and broker health](references/rocketmq-operations.md) |
| Pulsar | [Topics, subscriptions, retention, and geo-replication](references/pulsar.md) | [Backlog, acknowledgements, redelivery, and storage](references/pulsar.md) |

For example, Kafka consumer lag starts with Kafka operations. If the evidence points to partition skew, add Kafka design guidance. A duplicate business effect starts with idempotency even if the broker has not been selected.

## SD and SDD boundary

System Design defines interaction style, broker/product/version decision, ownership, deployable topology, concrete topic/exchange/queue/stream/group naming contract, message schema/version and key/partition/group strategy, delivery and ordering guarantees, publish/consume consistency, retry/DLQ/replay, security, capacity, observability, operations, migration, and per-feature producer/consumer sequences. SDD/OpenSpec implements the approved adapters, handlers, transaction/ack code paths, configuration, migration tasks, telemetry, and tests without silently redefining topology or contracts.

## Companion skills

Invoke `exception-error-standard` for failure taxonomy and boundary behavior, `log-trace-standard` for operational/audit events and producer/consumer propagation and links, and `cache-standard` only when messaging drives cache invalidation or materialization.

## Expected output

Include a brief numbered record of steps 1 through 7 with the outcome and evidence or next action for each step. Explain any `Not applicable` or `Blocked` outcomes.

Report the affected decisions, evidence, and unresolved risks. For a full messaging design, include applicable ownership, contracts, topology, publish and consumer semantics, retry and recovery, broker settings, security, capacity, observability, rollout, and verification.
