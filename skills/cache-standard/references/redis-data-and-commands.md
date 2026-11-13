# Redis Data and Commands

## Choose the data type from the operations

| Need | Candidate and trade-off |
|---|---|
| Fetch an opaque value or increment a counter | String. Bound encoded bytes. Use an atomic increment when a read/modify/write would race. |
| Read and update fields independently | Hash, or JSON when supported and nested path access matters. Check field versus whole-key expiry, returned payload size, and the cost of field growth. |
| Push and pop ordered values | List. Bound length. For durable processing with acknowledgement, evaluate Streams and the message contract. |
| Exact membership, uniqueness, or set operations | Set. Bound cardinality and the cost and slot placement of multi-key operations. A probabilistic filter is suitable only where its error behavior is acceptable. |
| Ranking or score/time windows | Sorted set. Specify tie behavior, window trimming, and range limits. |
| Compact flags, approximate distinct counts, or spatial lookup | Bitmap/bitfield, HyperLogLog, or geospatial indexes when their bounds and accuracy fit. Validate expected memory and error behavior. |

Check available types, exact complexity, cardinality, bytes returned, and expiry granularity for the deployed product. [Redis data types](https://redis.io/docs/latest/develop/data-types/)

## Choose the smallest command mechanism that preserves correctness

| Need | Mechanism and constraints |
|---|---|
| Update or create a key only when a condition holds | Prefer a single atomic command, such as `SET` with an appropriate condition and expiry option. Verify exact semantics and the result on a rejected condition. |
| Execute a fixed group without interleaving | `MULTI/EXEC`. Commands are queued, then executed together. An execution-time error does not roll back other commands. Inspect each result. |
| Reject a write if a value changed since reading it | `WATCH` with `MULTI/EXEC`. Handle aborted transactions with bounded retries and an explicit conflict outcome. Keep the watched operation on the correct client connection. |
| Apply conditional logic to several Redis operations atomically | Lua scripts or Redis Functions. Declare all accessed keys and respect cluster slot constraints. Keep execution bounded. Atomic execution does not imply rollback on runtime errors or atomicity with external systems. |
| Reduce network round trips for independent commands | Pipeline bounded batches. Pipelining does not add atomicity. Limit queued requests and replies, inspect failures individually, and handle an uncertain result after disconnect. |

Use versioned namespaces or explicit indexes for regular invalidation. For administrative inspection, incremental `SCAN` can return duplicates and does not provide a stable snapshot under mutation. Scope and bound the work and inspect the relevant primaries in a cluster. Avoid `KEYS`, unbounded ranges, and large synchronous deletes on latency-sensitive paths.

[Transactions](https://redis.io/docs/latest/develop/using-commands/transactions/) · [Pipelining](https://redis.io/docs/latest/develop/using-commands/pipelining/) · [Programmability](https://redis.io/docs/latest/develop/programmability/) · [SCAN](https://redis.io/docs/latest/commands/scan/)
