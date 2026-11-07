# Clean Code Review Checklist

Report each item as `Pass`, `Gap`, `Needs decision`, or `Not applicable`. Separate correctness defects, maintainability risks, and optional preferences.

- Approved behavior, language/paradigm, project conventions, scope, and verification baseline are known.
- Names reveal intent, avoid misinformation, distinguish concepts, are pronounceable/searchable, and use consistent problem/solution vocabulary.
- Public and long-lived names expose units, lifecycle, side effects, fallibility, or scope when types/context do not.
- Functions/modules are cohesive, operate at understandable abstraction levels, and do not contain unjustified pass-through indirection.
- Arguments and dependencies are explicit; flags, parameter objects, mutation, and global state are justified.
- The normal flow is easy to follow; branching, nesting, predicates, and state transitions are clear.
- Failures use language-idiomatic typed mechanisms; catch/translation/context/cleanup and caller needs are correct.
- Nullability and absence are explicit; callers are not forced to guess about `null` or sentinel values.
- Side effects, resource ownership, transactions, concurrency, cancellation, and lifecycle are visible.
- Duplication represents shared knowledge before it is abstracted; speculative abstractions and dead code are absent.
- Comments explain only remaining non-obvious contracts, intent, invariants, risks, or workarounds and are current.
- SOLID, patterns, and layered architecture are invoked only when concrete evidence warrants them.
- Formatting, lint/type/static checks, tests, and project-required verification pass or limitations are reported accurately.
- The change remains within approved scope and does not silently alter architecture or external contracts.
