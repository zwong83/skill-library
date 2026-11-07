# Risk, Portfolio, and Techniques

## Risk-Based Planning

For each risk record source requirement or design decision, affected journey/component, failure, likelihood, impact, detectability, exposure, controls, selected tests, owner, evidence, and residual risk. Prioritize catastrophic or irreversible impact even when likelihood is low.

Change impact should include direct code, callers, consumers, schemas, data, configuration, dependencies, permissions, operations, and rollback paths.

## Test Portfolio

| Level/type | Best evidence |
|---|---|
| Static analysis/review | Defects in requirements, design, code, dependencies, and configuration without execution |
| Unit/component | Local rules, algorithms, state, boundaries, and error behavior with fast diagnosis |
| Integration | Real adapter, database, broker, cache, filesystem, runtime, or dependency interaction |
| Contract | Producer/consumer compatibility and protocol/schema expectations |
| System/end-to-end | Critical cross-component journeys and deployed-system behavior |
| Acceptance | Product/business acceptance with accountable stakeholders or executable criteria |
| Non-functional | Security, performance, resilience, accessibility, compatibility, migration, and operability qualities |

No fixed ratio is universally correct. A test pyramid, trophy, or honeycomb is a heuristic; select the portfolio from coupling, risk, speed, fidelity, and diagnostic value.

## Scenario Design

Cover as applicable:

- happy path and alternate valid flows;
- equivalence partitions and boundary values;
- decision tables and business-rule combinations;
- state transitions and invalid transitions;
- missing, malformed, duplicate, stale, unauthorized, and conflicting input;
- concurrency, ordering, idempotency, timeout, cancellation, and partial outcome;
- dependency failure, overload, degradation, recovery, and reconciliation;
- old/new version coexistence, migration, rollback, and replay;
- invariant or property-based exploration and fuzzing for broad input spaces.

Specify the oracle: exact expected state, output, side effect, absence of forbidden effects, telemetry, and cleanup. “Works correctly” is not an oracle.

## Coverage

Trace requirement, risk, state, decision, branch, interface, and failure-mode coverage where each is meaningful. Line or branch coverage can expose untested code but does not prove useful assertions. Use mutation or fault injection selectively to assess whether tests detect meaningful behavioral changes.

## Primary References

- [ISTQB CTFL v4.0](https://www.istqb.org/certifications/certified-tester-foundation-level-ctfl-v4-0/)
- [ISTQB CTFL Syllabus v4.0.1](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf)
- [The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
