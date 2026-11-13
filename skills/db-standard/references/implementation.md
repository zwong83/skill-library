# Database implementation and DML routing

Use this mode for connections and pools, SELECT/INSERT/UPDATE/DELETE, CRUD, transactions, isolation, locking, concurrency, pagination, batching, query optimization, persistence frameworks, vendor-specific SQL, and database access tests.

First inspect the project's driver, connection configuration, pool, transaction boundary, framework, repository/DAO/mapper conventions, migrations, and existing SQL. Extend those conventions rather than introducing a competing framework. Keep queries parameterized, avoid unsafe string concatenation and unnecessary dynamic SQL, and make update/delete predicates intentional. Check affected rows when stale writes, idempotency, or data integrity depends on them.

For performance work, inspect the query shape, cardinality, predicates, joins, ordering, indexes, execution plan, statistics, locks, and production-like data volume before changing code. For pagination, choose an approach appropriate to stable ordering and scale; avoid offset pagination when its cost or consistency characteristics are unacceptable. For transactions and concurrency, state the boundary, isolation assumptions, lock behavior, retry/idempotency needs, and failure handling.

This reference does not replace exact framework or database documentation. When behavior depends on a vendor/version, verify it against the project's authoritative documentation and version, and test the behavior in a safe environment.
