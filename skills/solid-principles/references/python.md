# SOLID in Python

- Review responsibility at module, class, callable, and package boundaries.
- Use duck typing or `Protocol` when consumers need a structural contract; use abstract base classes only when shared lifecycle or nominal membership is meaningful.
- Functions, closures, decorators, generators, and context managers may express extension and inversion more clearly than class hierarchies.
- LSP includes exceptions, mutability, return shapes, sync/async behavior, context-manager behavior, and resource ownership.
- Avoid class-per-operation designs and dependency-injection frameworks when explicit parameters or module composition are sufficient.
- Use dataclasses and immutable values for data semantics; do not attach behavior merely to satisfy an OOP style.
