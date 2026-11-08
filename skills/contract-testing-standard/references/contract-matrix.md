# Contract Matrix

| Contract case | Required fields |
|---|---|
| Provider/consumer identity | owner, repository/service, supported version, lifecycle status |
| Operation/message | method/topic/type, request/payload, response/result, error contract, side effects |
| Evolution | base/target versions, compatibility promise, deprecation/removal window, migration owner |
| Test case | TA/source IDs, positive/negative/boundary category, fixture, expected compatibility result |
| Verification | publisher, verifier, environment/registry, command/job, retained evidence, verdict |

Cover required/optional/null/omitted/default values, ranges and lengths, unknown fields, enums, repeated/map fields, ordering, content types/encoding, stable errors, authentication metadata where contractual, and duplicate/idempotent semantics where consumers rely on them.
