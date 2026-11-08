# Environment, Data, and Evidence

Record deployed component revisions, topology, configuration/features, dependency endpoints/versions, clocks, identity provider, tenant model, observability, and known fidelity differences. Shared environments require namespace/tenant/data isolation and ownership.

Create deterministic synthetic data with a unique run identity. Coordinate asynchronous completion through observable state/events with bounded deadlines. Clean up records, messages, files, cache keys, test identities, and external fixtures even after failure; report incomplete cleanup.

Retain the smallest useful correlated evidence: run ID, component versions, journey steps, authoritative state, events, logs/traces/metrics, screenshots when applicable, failures, retries, and cleanup. Redact credentials, tokens, personal data, and private production content.
