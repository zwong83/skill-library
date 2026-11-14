# Object-Oriented Refactoring Guide

Refactor from observed change pain, defects, or testability constraints. Preserve behavior unless an approved requirement changes it.

## Workflow

1. Identify the concrete smell and evidence: change history, defects, dependency cycles, test setup, duplicated rules, unstable interfaces, or unsafe state.
2. Characterize current behavior with tests or other evidence before structural change.
3. Identify the violated responsibility, invariant, ownership, or dependency boundary.
4. Choose the smallest refactoring that improves that boundary.
5. Make one reviewable change at a time and rerun relevant verification.
6. Remove obsolete abstractions, adapters, dead code, and temporary compatibility paths when safe.
7. Update SD/SDD/ADR artifacts when architectural or contract decisions change.

## Common symptoms and responses

| Symptom | Investigate | Possible response |
|---|---|---|
| God object/service | Unrelated change drivers and dependencies | Extract coherent responsibility or policy; retain explicit orchestration |
| Anemic model | Rules implemented far from owned data/invariants | Move invariant-protecting behavior to the owning boundary |
| Feature envy | Method mostly reads another object's internals | Move behavior, expose a meaningful operation, or revise ownership |
| Shotgun surgery | One change touches many unrelated locations | Centralize the rule or stabilize a boundary |
| Primitive obsession | Invalid combinations and repeated validation | Introduce a validated value or domain type |
| Inappropriate inheritance | Type checks, disabled methods, broken semantics | Replace with composition, delegation, traits, or explicit variants |
| Fat interface | Consumers use unrelated subsets | Split by consumer role and contract |
| Hidden dependency | Globals, service locators, implicit framework access | Make dependency and lifecycle explicit |
| Leaky abstraction | Consumers depend on implementation details | Redefine the contract or remove the unhelpful abstraction |

Do not treat every long method, large class, switch, or concrete dependency as a violation. Evaluate behavior, volatility, contract stability, and the cost of additional indirection.
