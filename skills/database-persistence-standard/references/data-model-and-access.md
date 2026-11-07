# Data Model and Access

## Ownership and Source of Truth

For every dataset identify its authoritative writer, permitted readers, replication or projection paths, tenant scope, classification, retention, deletion owner, and reconciliation mechanism. Avoid multiple services directly updating the same tables unless shared ownership is an explicit architectural decision.

## Store Selection

| Store | Suitable signals | Risks to resolve |
|---|---|---|
| Relational database | Strong constraints, transactions, joins, structured operational data | Hot rows, migration discipline, query/index design, scale topology |
| Document database | Aggregate-shaped documents, flexible evolution, document-local access | Cross-document invariants, query patterns, document growth, consistency |
| Key-value store | Known-key access, high throughput, simple state | Secondary access, scans, atomicity scope, expiry and eviction |
| Search engine | Full-text search, ranking, faceting, read projections | Not usually source of truth, refresh lag, reindexing, mapping evolution |
| Object storage | Large immutable or append-oriented blobs | Metadata authority, lifecycle, integrity, access control, orphan cleanup |

State why the chosen system fits better than the existing default. Include operational maturity, backup, restore, observability, cost, and team ownership.

## Logical and Physical Model

Define:

- stable identity and natural versus surrogate keys;
- attributes, types, precision, units, time zone, normalization, and encoding;
- required, optional, nullable, default, generated, and immutable fields;
- relationships, cardinality, ownership, cascade behavior, and orphan handling;
- uniqueness, check, foreign-key, and exclusion constraints where supported;
- tenant partitioning and row-level isolation expectations;
- creation, update, version, soft-delete, retention, and audit fields;
- large-object placement, history, archival, and erasure behavior.

Do not copy API schemas directly into tables. API, domain, and persistence models evolve for different reasons.

## Queries and Access Paths

Inventory critical reads and writes with filter, join, sort, group, expected cardinality, frequency, latency target, and consistency need. For each critical query:

- bind parameters; never concatenate untrusted input into SQL;
- return only needed fields and bounded rows;
- define deterministic ordering and pagination;
- identify the supporting key or index and its selectivity;
- verify the execution plan with representative statistics and data volume;
- account for write amplification, index maintenance, storage, and lock impact;
- detect N+1 and fan-out behavior at repository and service boundaries.

Index foreign keys and search predicates only when workload evidence supports it; avoid speculative indexes. Re-evaluate plans as data distribution changes.

## Pagination and Batching

Offset pagination may be acceptable for small, stable datasets. For changing or large datasets, prefer a stable cursor built from a deterministic sort and tie-breaker. Define behavior for deleted or inserted rows, cursor expiry, maximum page size, and backward navigation.

Batch writes and reads within datastore and driver limits. A larger batch is not always faster and may enlarge locks, transactions, memory, or retry cost.

## Connections and Drivers

- Bound pool size from application concurrency and database capacity, not arbitrary defaults.
- Define acquisition, statement, transaction, socket, idle, and lifetime timeouts where supported.
- Validate stale-connection handling and rotation during database failover.
- Keep credentials outside code and scope them to required schemas and operations.
- Monitor pool saturation, wait time, active connections, slow queries, errors, deadlocks, and replica lag.
