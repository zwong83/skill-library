# SOLID in C#

- Use namespaces, classes, interfaces, records, structs, delegates, events, pattern matching, generics, and dependency injection according to the boundary.
- Include nullability, exceptions, async/cancellation behavior, disposal, thread safety, event subscription, and enumeration semantics in LSP review.
- Prefer records or immutable values for value semantics and discriminated/pattern-based approaches for intentionally closed variants.
- Split interfaces by coherent consumer role and lifecycle, not by arbitrary method-count limits.
- DI registration does not prove DIP; high-level policy should own stable contracts and remain independent of infrastructure mechanisms.
- Avoid wrappers and interface pairs that add indirection without substitution, testing, ownership, or architectural value.
