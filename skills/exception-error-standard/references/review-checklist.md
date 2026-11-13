# Error Handling Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- Material failure modes and terminal outcomes are identified.
- Error categories and stable codes are distinct and actionable.
- Every application-defined error and exception uses an enum member with a stable integer `code` and a non-empty, safe text `message`. Exceptions and typed results for the same failure reuse the same member.
- Boundaries serialize the enum's `code` as a number and `message` as text in formats that support numeric fields. Preserve published contracts. Unmapped failures use the internal-error member with the cause retained in protected diagnostics.
- Expected business outcomes use an idiomatic typed contract rather than accidental generic exceptions.
- Each domain exception has one reusable type in its owning domain. Call sites reuse it and construct a fresh instance for each occurrence.
- Specialized subclasses express a distinct domain failure or handling requirement and preserve the parent contract.
- Throw/return, catch, translation, and final-handling ownership are explicit.
- Domain/application contracts do not leak transport or vendor error types.
- Original causes are preserved safely and failures are not swallowed.
- Public errors exclude stack traces, secrets, sensitive payloads, queries, and topology.
- Retryability is classified; retries are bounded, budget-aware, and safe for side effects.
- One layer owns retries, preventing multiplicative retry storms.
- API, job, scheduler, and message-consumer boundary mappings are complete.
- Errors are logged once at the owning boundary and correlated with traces.
- Tests cover translation, cancellation, timeout, retry exhaustion, duplicate processing, cleanup, and redaction.
