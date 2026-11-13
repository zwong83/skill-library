# Database design

Translate business rules and access patterns into a correct, consistent, performant, scalable, and maintainable model. Identify entities, attributes, lifecycle, ownership, relationships, constraints, and important queries before finalizing tables.

Choose keys deliberately among natural keys, surrogates, UUIDs, distributed IDs, sequences, and auto-increment values. Consider uniqueness, ordering, storage and index size, generation, and distributed operation. Model one-to-one, one-to-many, and many-to-many relationships explicitly; use a junction table for many-to-many relationships unless a documented alternative is justified.

Use primary keys, foreign keys, unique, not-null, and check constraints for fundamental integrity where supported. Normalize by default; denormalize only for a documented read, aggregation, query-complexity, or scale benefit. Derive indexes from actual WHERE, JOIN, ORDER BY, GROUP BY, uniqueness, and projection patterns, and account for write cost and selectivity.

Prefer backward-compatible schema evolution: add compatible structure, deploy compatible code, backfill safely, switch behavior, and remove old structure later. Validate entities, relationships, keys, constraints, nullability, access-pattern indexes, transaction/concurrency needs, expected volume, growth, and migration path.
