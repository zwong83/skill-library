# System Design Specialist Coordination

The System Design Coordinator owns the source baseline, routing, conflicts, final document, readiness status, and approval boundary. Specialists never edit the final SD directly unless the Coordinator explicitly assigns a bounded section; they return decision packets.

## Shared inputs

Provide each selected specialist only the relevant subset of:

- design context and scope;
- governing SA and requirement IDs;
- confirmed constraints and approved decisions;
- routing matrix with `Required`, `Conditional`, or `Not Applicable` status;
- relevant existing design/code facts;
- unresolved items and explicit deferrals;
- requested packet destination.

## Decision packet

Every packet contains:

1. Scope and sources reviewed.
2. Specialized skills and references actually loaded.
3. Proposed decisions with stable IDs and approval status.
4. Alternatives, rationale, trade-offs, and consequences.
5. Contracts, targets, diagrams, or models needed for that specialty.
6. Dependencies on other packets and assumptions received from them.
7. Conflicts, unresolved decisions, risks, and owners when known.
8. Requirement-to-decision-to-verification traceability.

Write cross-specialty conflicts to the conflict register; do not silently resolve or overwrite another packet. Specialists may request information through the Coordinator, not through an unrestricted peer-to-peer loop.

## Merge and review

The Coordinator reconciles packets into one SD and records accepted/rejected proposals. The Review Agent receives the merged draft, source baseline, routing matrix, decision/conflict/open registers, and specialist packets. It reports gaps but does not redesign the system or approve unresolved decisions.
