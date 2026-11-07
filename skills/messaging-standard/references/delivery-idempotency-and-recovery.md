# Delivery, Idempotency, and Recovery

## Publish coordination

A database commit and broker publish are not one atomic action by default. Define the loss/duplication windows. Common approaches include:

- transactional outbox plus idempotent relay;
- change-data capture from an owned outbox/change log;
- broker transaction when its exact boundary covers the required state;
- explicit reconciliation when occasional divergence is accepted.

Do not use an uncoordinated `commit database -> publish` sequence while claiming no-loss delivery.

## Consumer processing

For each consumer define:

1. validation and compatibility handling;
2. deduplication/idempotency key and retention window;
3. transaction and side-effect boundary;
4. acknowledgement or offset-commit point;
5. retryable versus terminal errors;
6. partial batch behavior;
7. poison-message quarantine/dead-letter behavior;
8. replay and reconciliation procedure.

Idempotency can use natural idempotent state transitions, unique constraints, inbox/dedup records, conditional updates, or destination-supported idempotency keys. A volatile in-memory set is insufficient across restart unless loss is accepted.

## Ordering and concurrency

State the required scope: none, per entity/key/group/partition, per producer, or global. Select a stable key that captures the invariant. Ordered processing reduces parallelism and can cause head-of-line blocking; define retry behavior without silently reordering dependent events.

## Retries and dead letters

- Bound attempts, delay/backoff, jitter, age, and total processing deadline.
- Separate transient dependency failures from malformed, unauthorized, incompatible, and deterministic business failures.
- Prevent hot requeue loops and multiplicative application/broker retries.
- Define DLQ/quarantine owner, alert, metadata, sensitive-data controls, retention, inspection, correction, replay idempotency, and deletion.
- Replaying an old contract must not bypass current authorization, validation, or migration rules.

## Observability

Measure publish acceptance/failure, end-to-end age, queue/partition lag, processing latency, retries/redeliveries, dedup hits, poison messages, DLQ depth, consumer availability, rebalance/failover, and replay progress. Correlate producer and consumer spans according to `tracing-standard`.
