# SOLID Limitations and False Positives

SOLID is most useful for object-oriented or modular designs with meaningful contracts and change pressure. It is not a universal optimization target.

## Common false positives

- A large cohesive type is not automatically an SRP violation.
- A `switch` over a deliberately closed set is not automatically an OCP violation.
- A concrete dependency is not automatically a DIP violation.
- A multi-method interface is not automatically an ISP violation.
- Different implementation performance is not automatically an LSP violation unless the contract or consumer expectation makes it material.
- Fewer abstractions are not automatically less maintainable.

## Costs to include

- more types, files, indirection, configuration, allocation, runtime dispatch, and framework wiring;
- harder navigation, debugging, ownership, and onboarding;
- abstraction leakage or contracts weaker than the implementation they hide;
- speculative extension points that constrain rather than enable future change.

## Stop condition

Recommend no refactor when the current design is coherent, behaviorally correct, testable in proportion to risk, native to the language, and cheaper to evolve than the proposed abstraction.

SOLID findings should identify a real consumer, contract, change driver, or dependency problem. Without evidence, label the suggestion optional rather than a violation.
