# API Documentation and Docstrings

Document the consumer-visible contract rather than rephrasing the signature.

Include as applicable:

- purpose and intended consumer;
- parameter meaning, units, ranges, formats, and ownership;
- return value, absence/null behavior, and mutation;
- errors/exceptions and when they occur;
- side effects, transactions, I/O, caching, and security implications;
- thread/async safety, cancellation, blocking, lifecycle, and cleanup;
- idempotency, ordering, compatibility, and versioning;
- concise example when correct use is otherwise unclear.

Avoid duplicating information already precise in names and types. Keep implementation details out of public contracts unless consumers must rely on them. Use the language's standard documentation format so tooling, IDEs, and generated API docs can consume it.

For overrides/implementations, inherit documentation when the contract is unchanged; document only meaningful specialization. A subtype must not silently weaken the documented contract.

For generated code, update comments in the generator or template so regeneration preserves the documentation.
