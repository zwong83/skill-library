# SOLID in Java and JVM Languages

- Use packages/modules, interfaces, records/data classes, sealed hierarchies, enums, lambdas, and dependency injection according to the actual variation.
- Constructor injection makes dependencies visible, but it does not by itself establish correct dependency direction or coherent responsibility.
- Avoid an interface/implementation pair when there is no consumer boundary, substitution, external mechanism, or architectural need.
- Prefer immutable values and sealed variants where the set of cases is intentionally closed; OCP does not require every `switch` to become Strategy.
- Treat exceptions, nullability, transactions, thread safety, blocking behavior, and framework lifecycle as part of substitutability.
- In Kotlin or Scala, prefer native sealed types, functions, traits, and immutable data over mechanically translated Java class patterns.

Framework annotations are wiring and runtime metadata. They do not prove SRP, OCP, LSP, ISP, or DIP.
