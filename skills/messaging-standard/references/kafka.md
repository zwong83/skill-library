# Kafka Guidance

Apply only when Apache Kafka and the deployed broker/client versions are selected.

- Define topic ownership, partitions, replication/durability expectations, retention/compaction, record key, consumer groups, schema governance, ACLs, quotas, and migration strategy.
- Ordering is within a topic partition. Choose a key that keeps records requiring order in the same partition and assess skew/hot partitions. See [Apache Kafka documentation](https://kafka.apache.org/documentation/).
- Define producer acknowledgement, idempotence, retries, delivery timeout, batching, compression, and error handling from the installed client version. Do not copy configuration defaults across versions.
- Idempotent production prevents specific duplicate writes within Kafka producer semantics; transactions can atomically include produced records and consumed offsets. They do not automatically make external database/API side effects exactly once.
- For consume-process-produce flows requiring Kafka transactional semantics, define transactional IDs, producer lifecycle/fencing, offset participation, and `read_committed` consumer isolation. Kafka documents the scope and external-system limitations in [Kafka design: exactly-once semantics](https://kafka.apache.org/42/design/design/#semantics).
- For external side effects, coordinate offsets with destination state, use idempotent writes/inbox records, or provide reconciliation. Avoid auto-commit before processing when that would permit loss.
- Define rebalance behavior, processing-time limits, batch partial failure, poison records, retry topics or application retry state, DLQ/quarantine, replay offsets, and retention compatibility. Kafka does not make these application policies correct automatically.
- Monitor producer errors, record/send latency, under-replication and broker health, consumer lag and record age, rebalances, processing time, retries, transaction aborts/fencing, hot partitions, DLQ, and replay progress.
