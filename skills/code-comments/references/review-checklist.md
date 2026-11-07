# Comment Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`.

- The comment answers a real reader question not already clear from code, types, tests, or design docs.
- It explains intent, contract, invariant, risk, rationale, or non-obvious mechanism rather than narrating syntax.
- It is placed at the boundary it governs and uses the language's standard format.
- Public documentation covers consumer-visible errors, side effects, lifecycle, concurrency, units, and compatibility where relevant.
- The comment matches all current code paths and has been updated with the change.
- Links/references are stable and sufficient without copying large external documents.
- TODO/FIXME is actionable and does not hide required current-scope work.
- No secrets, sensitive data, private incident details, blame, or misleading historical narrative is present.
- No dead/commented-out code remains.
- A clearer name, type, extraction, test, or design document is not a better solution.
