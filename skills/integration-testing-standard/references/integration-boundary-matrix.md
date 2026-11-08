# Integration Boundary Matrix

| Boundary | Representative concerns |
|---|---|
| Relational/document store | Mapping, constraints, queries, transactions, isolation, migrations, indexes/plans where required |
| Cache | Serialization, keys, TTL, invalidation, consistency, eviction/provider failure |
| Broker/stream | Contract, publish coordination, delivery, acknowledgement/offset, ordering, duplicate, retry, DLQ, replay |
| HTTP/gRPC/GraphQL | Serialization, validation, authentication/authorization, status/error mapping, deadlines, compatibility |
| Files/object storage | Paths/keys, metadata, integrity, permissions, lifecycle, partial failure, cleanup |
| Framework/runtime | Routing, dependency injection, middleware/interceptors, configuration binding, transaction/proxy behavior |
| External provider | Contract sandbox/test instance, authentication, timeouts, error mapping, rate limits, webhooks/callbacks |

For each selected boundary record source/risk IDs, real components, mocked components, versions/config, setup, input, expected state/output/effects, failure/recovery, cleanup, and evidence.

Use contract tests when consumer/provider compatibility is the risk; use broader end-to-end tests only when the real multi-component journey cannot be proven at a narrower boundary.
