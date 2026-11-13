# Message Contracts and Compatibility

## Message classification

- **Command:** asks one owning capability to perform an action; name imperatively and avoid multiple competing owners.
- **Domain/integration event:** states a fact that occurred; name in past tense and keep producers unaware of consumer workflows.
- **Notification:** informs recipients without becoming the authoritative business record.
- **Stream record:** represents an ordered or retained data change for replay/materialization.
- **Request/reply:** introduces temporal and correlation coupling; use only when asynchronous request/reply is intentional.

## Envelope

Define fields only when meaningful and approved:

| Field | Purpose |
|---|---|
| `message_id` | Stable identity for deduplication and investigation |
| `message_type` | Stable low-cardinality contract name |
| `schema_version` | Compatibility and decoding decision |
| `occurred_at` | When the business fact occurred |
| `produced_at` | When the record was emitted, if different |
| `producer` | Owning capability/service identity |
| `correlation_id` / `causation_id` | Business workflow relationship when required |
| trace context | Diagnostic propagation according to tracing standards |
| ordering/partition key | Scope for ordered processing and distribution |
| tenant/data classification | Isolation and handling policy when approved |
| payload | Minimal business contract, not an internal object dump |

Do not use message IDs, correlation IDs, or trace IDs as authentication or authorization evidence.

## Compatibility

- Assign one owner for each contract and maintain a consumer inventory.
- Prefer additive backward-compatible evolution; define defaults for absent fields and behavior for unknown fields/types.
- Separate semantic versioning decisions from serializer/wire-format versioning.
- Use a schema registry or equivalent governance when multiple teams/languages share contracts and compatibility enforcement adds value.
- Define deprecation window, dual-read/write needs, consumer migration order, rollback, retention/replay compatibility, and tombstone/deletion semantics.
- Classify and minimize data; define encryption, retention, deletion, regional/tenant boundaries, and consumer authorization.
