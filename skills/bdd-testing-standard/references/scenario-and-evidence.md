# Scenario and Evidence Example

For an approved FRS feature whose acceptance rule says withdrawals cannot exceed the available balance, an example is:

```gherkin
Feature: Withdraw available funds
  @AC-17 @BDD-17-1
  Scenario: Reject a withdrawal exceeding the available balance
    Given an account has an available balance of 100
    When the customer requests a withdrawal of 150
    Then the withdrawal is rejected for insufficient funds
    And the available balance remains 100
    And no withdrawal is posted to the ledger
```

The no-ledger-effect assertion belongs only if the approved rule includes it. Do not silently invent policy for fees, overdrafts, holds, currency precision or concurrent withdrawals. Record those questions with their owners. Add approved below/at/above-limit examples and other relevant partitions; one rejection scenario does not cover the entire withdrawal feature.

| Field | Example meaning |
|---|---|
| Source and approval | FRS feature F-17 and acceptance AC-17, approved FRS version; name an equivalent approved source if no FRS exists |
| Delivery scope and readiness | Selected increment; record whether F-17 is implemented and executable, retaining required unimplemented cases and approved deferred features separately |
| Scenario / case | BDD-17-1 linked to the existing TA case if supplied |
| Authoritative scenario set | One maintained feature file or approved FRS scenario location/version, referenced by both implementation and testing |
| Underlying boundary | Integration through the service and real test database when ledger durability is the claim |
| Owner | BDD testing for this assigned case; retain TDD ownership if its cycle is active |
| Assets | Existing feature, binding and fixture paths; reuse tests where they prove the same obligation |
| Data and cleanup | Isolated account/ledger data and deterministic reset, with no real customer withdrawals |
| Evidence | Exact revision, environment, runner command and scenario result; leave unrun until observed |

If only the domain decision is unit-tested with a fake ledger, report that narrower proof and retain the real-boundary gap. Do not add duplicate UI/E2E coverage unless a distinct approved journey risk requires it. If the scenario is owned by an existing integration/E2E specialist, link its test and evidence rather than assigning a second owner or editing its files concurrently.

Undefined steps, a discovery-only run or an all-skipped suite cannot produce BDD-Passed. For review-only work retain original run provenance and state that no new execution occurred.

For example, implementation may consume BDD-17-1 from the maintained withdrawal feature file and map its cycle tests to that ID. Acceptance testing later executes the same scenario through its bindings and records a new result for the target build. Neither phase needs a copied scenario document. A new runner may change bindings without changing the business scenario; an approved overdraft policy change requires a traceable scenario revision and revalidation of affected tests/evidence.
