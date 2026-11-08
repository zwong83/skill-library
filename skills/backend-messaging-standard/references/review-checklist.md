# Messaging Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Message type, purpose, owner, consumers, authority, and lifecycle are explicit.
- Contract envelope, schema, compatibility, deprecation, privacy, and replay rules are defined.
- Broker choice follows durability, ordering, latency, throughput, replay, retention, and operational requirements.
- Publish coordination identifies database/broker loss and duplication windows.
- Delivery guarantees are scoped end to end without an unsupported exactly-once claim.
- Consumers are idempotent and acknowledge/commit only after required durable effects.
- Ordering key/scope, concurrency, skew, head-of-line blocking, and retry interaction are addressed.
- Retry ownership, timeout, backoff, limits, terminal errors, and partial batch behavior are explicit.
- DLQ/quarantine has ownership, alerting, access, retention, diagnosis, correction, replay, and deletion procedures.
- Broker-specific topology and settings are tied to verified deployed versions.
- RocketMQ designs distinguish 4.x/5.x broker, Proxy, client, message-type, retry, transaction, and HA behavior when applicable.
- Authentication, authorization, encryption, tenant/data classification, quotas, and retention are defined.
- Metrics, logs, traces, alerts, capacity, failover, migration, rollback, and operational ownership are complete.
- Production runbooks cover ambiguous sends, missing/duplicate messages, backlog drain, retry storms, DLQ recovery, replay/offset changes, disk pressure, failover, and upgrades where applicable.
- Tests cover duplicates, loss windows, delay, reordering, poison messages, failover/rebalance, schema evolution, and replay.
