# Coordination and Idempotency

## Lock and lease contract

Use local request coalescing when it meets the refill requirement. For work shared across instances, first consider whether partitioning or making the operation idempotent removes the need for a lock. When a lock is needed, define the owner, acquisition timeout, lease expiry, renewal, conditional release, and behavior on crash or partition. Record whether duplicate work is harmless or whether the resource must reject stale owners.

For election or singleton scheduling, define failure detection, re-election, split-brain handling, and whether the job can safely run twice. Select only the mechanism below that applies.

## Redis lease

Acquire atomically with set-if-absent and expiry, using a unique owner token per acquisition. Renew and release atomically only if the token still matches. Assess process pauses, expiry races, and whether a Redis failover or replication lag can permit concurrent owners. Use resource-side validation when a stale owner can violate a business invariant.

## Fencing stale owners

Use a monotonically increasing fencing token on ownership changes, or an equivalent version check. The protected resource must reject operations from stale owners as part of accepting the write. A random lease owner token supports conditional release and renewal. It does not order ownership changes. Verify that a paused worker cannot overwrite work after a new owner takes over.

## Cache-backed deduplication

Scope a stable key to the operation and caller or tenant. Define how concurrent attempts, in-flight duplicates, completed duplicates, unknown outcomes, partial effects, and retention expiry are handled. A timed-out attempt may already have applied its effect. Reconcile uncertain outcomes before repeating work when it could duplicate that effect.

Treat a cache record as a best-effort optimization when it can expire, be evicted, or be lost during restart or failover. For a business effect that must occur only once, enforce uniqueness at the durable effect boundary or use the destination's idempotency contract. For broker redelivery, use [message idempotency](../../message-standard/references/idempotency.md).

## Other coordination backends

- **etcd:** Use leases, revisions, compare-and-swap transactions, watches, and quorum-backed reads as applicable. Define lease expiry, watch compaction and recovery, quorum loss, revision ordering, and member health. Bound values and write rates. Monitor leader changes, proposal latency, database size, and alarms.
- **ZooKeeper:** Use ephemeral nodes, sessions, and watches as applicable. Define session expiry, watch re-registration, ensemble quorum, split-brain prevention, and herd effects. Require resource-side safety when a stale owner could cause harm.

## Verification and signals

Verify contention, owner crash, expiry, failed renewal, stale writes, and duplicate attempts only where those paths apply. Track acquisition latency, contention, timeout, renewal failure, election status, and leader changes for the selected mechanism. Alert when an operator can act.
