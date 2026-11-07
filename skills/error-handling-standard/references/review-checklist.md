# Error Handling Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Material failure modes and terminal outcomes are identified.
- Error categories and stable codes are distinct and actionable.
- Expected business outcomes use an idiomatic typed contract rather than accidental generic exceptions.
- Throw/return, catch, translation, and final-handling ownership are explicit.
- Domain/application contracts do not leak transport or vendor error types.
- Original causes are preserved safely and failures are not swallowed.
- Public errors exclude stack traces, secrets, sensitive payloads, queries, and topology.
- Retryability is classified; retries are bounded, budget-aware, and safe for side effects.
- One layer owns retries, preventing multiplicative retry storms.
- API, job, scheduler, and message-consumer boundary mappings are complete.
- Errors are logged once at the owning boundary and correlated with traces.
- Tests cover translation, cancellation, timeout, retry exhaustion, duplicate processing, cleanup, and redaction.
