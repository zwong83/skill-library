# Contract-First Parallel Frontend Design

## Stage 1: backend domain baseline

Before detailed frontend design, require sufficiently stable backend ownership for domain rules, data/source of truth, transactions/consistency, server authorization, state transitions, and error categories. This need not be the complete backend SD.

## Stage 2: joint contract readiness

The Interface/Data packet proposes the service/API/event contract. The Frontend packet evaluates it against approved journeys and UI needs. The System Design Coordinator owns reconciliation and records `Contract-Ready` only when applicable operations, fields, errors, authorization context/results, idempotency, concurrency, pagination/filter/sort, limits, deadlines/cancellation, compatibility, examples, and ownership are resolved.

Frontend feedback should expose excessive request fan-out, unstable client-side joins, duplicated business rules, ambiguous field/error semantics, missing partial/loading/recovery behavior, unsafe retries, and unsupported navigation or optimistic-update needs. It must not move authoritative business rules into the client merely for convenience.

## Stage 3: parallel detail design

After `Contract-Ready`, backend and frontend specialists may refine their own boundaries in parallel from the versioned contract. They exchange decision IDs and packet summaries only through the Coordinator. Any material contract change reopens affected decisions, tasks, mocks/fixtures, contract tests, and readiness.

## Handoff

The final SD records backend authority, the accepted versioned contract, frontend decisions, cross-packet dependencies, compatibility/evolution, verification, and open items. Frontend implementation begins only through SDD after the merged SD is ready and implementation is separately authorized.
