# Message Delivery Semantics

At-most-once may lose messages but avoids intentional redelivery. At-least-once may duplicate and therefore requires idempotent business processing. Exactly-once must be evaluated across broker, consumer, database, and external side effects; broker-level guarantees alone do not prove exactly-once business outcomes.

Document the ACK/commit boundary and the recovery behavior for process crash, timeout, rebalance, and broker failure.
