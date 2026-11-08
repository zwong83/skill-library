# Contract-First Parallel Frontend Design

## Stage 1: backend domain baseline

Before detailed frontend design, require sufficiently stable backend ownership for domain rules, data/source of truth, transactions/consistency, server authorization, state transitions, and error categories. This need not be the complete backend SD.

## Stage 2: joint contract readiness

The Interface/Data handoff proposes the service/API/event contract. The Frontend handoff evaluates it against approved journeys and UI needs. The System Design Coordinator owns reconciliation and records `Contract-Ready` only when applicable operations, fields, errors, authorization context/results, idempotency, concurrency, pagination/filter/sort, limits, deadlines/cancellation, compatibility, examples, and ownership are resolved.

Frontend feedback should expose excessive request fan-out, unstable client-side joins, duplicated business rules, ambiguous field/error semantics, missing partial/loading/recovery behavior, unsafe retries, and unsupported navigation or optimistic-update needs. It must not move authoritative business rules into the client merely for convenience.

## Stage 3: parallel detail design

After `Contract-Ready`, backend and frontend specialists may refine their own boundaries in parallel from the versioned contract. They exchange only changed decision IDs and compact handoffs through the Coordinator. Any material contract change reopens affected decisions, tasks, mocks/fixtures, contract tests, and readiness.

## Handoff

Backend SD records backend authority and internals; Frontend SD records frontend decisions; Integration SD records the accepted versioned contract semantics, cross-boundary dependencies, compatibility/evolution, and contract verification; the Index records readiness and unresolved items. Frontend implementation begins only through SDD after the applicable SD set is `SD-Ready` and implementation is separately authorized.
