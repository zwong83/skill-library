# System Design Specialist Coordination

The System Design Coordinator owns the source baseline, routing, reconciliation, authoritative document set, readiness status, and approval boundary. Specialists return compact handoffs; they do not create persistent packet documents or edit authoritative SD files unless the Coordinator explicitly assigns a bounded section.

## Minimal context envelope

Provide each specialist only what it needs:

- requested concern and target document: Backend, Frontend, Integration, or Index;
- governing requirement/SA IDs and statuses, not full source restatements;
- current accepted decision IDs and contract version relevant to that concern;
- confirmed constraints and applicable existing-system facts;
- unresolved items that may affect the work;
- expected verification evidence.
- assigned feature IDs, required diagram IDs/views, current-system evidence, and artifact paths/versions.

Do not send unrelated source documents, other specialists' full reasoning, or the complete SD set when a stable ID, section link, contract fragment, or short accepted-decision summary is sufficient.

## Compact handoff contract

Return only these fields:

1. **Feature and diagram coverage** — feature IDs, required diagram IDs/views, As-Is/To-Be status, target document/section, and gaps.
2. **Accepted decisions** — stable ID, concise normative result, status, and target document/section.
3. **Artifact and contract changes** — affected contract/database/middleware artifact and version, exact semantic change, compatibility impact, and `None` when unchanged.
4. **Dependencies and impacts** — only new or changed cross-boundary dependencies, affected decision IDs, and required follow-up.
5. **Blockers** — unresolved decision, missing current evidence, impact, owner when known, and target document/artifact; use `None` when clear.
6. **Verification** — requirement/feature/diagram/decision/artifact-to-evidence mapping and readiness recommendation.

Return every assigned diagram/model fragment and authoritative DDL/DML/middleware artifact update needed by the target SD; these are design content, not optional packet decoration. Record material decisions with rationale and consequences, without solution-comparison tables. Omit repeated background, generic explanation, settled facts, unchanged content, rejected-option histories, duplicated schemas, and chain-of-thought.

The handoff is transient unless an audit requires retention. The Coordinator writes accepted content once into its target document and discards redundant handoff prose.

## Runtime delegation rules

Delegation is an execution mechanism, not a new artifact or ownership layer. A delegated specialist receives one minimal context envelope and returns one transient compact handoff. By default it must not edit the authoritative SD documents; the Coordinator remains their sole reconciler and writer.

Independent read-heavy concerns may run concurrently from the same validated baseline. Dependent stages remain ordered: backend ownership and draft contract before frontend contract review, shared contract reconciliation before parallel detail, and authoritative SD assembly before the Coordinator applies the quality gate. Any write-enabled delegation must have exclusive file or section ownership; otherwise run it sequentially.

Do not rely on hidden conversation state between specialists. Put every necessary source ID, accepted decision, contract version, constraint, blocker, and expected evidence item in the handoff envelope. If delegated Agents are unsupported, preserve the same boundaries and execute the specialists sequentially.

## Conflict and decision handling

Do not silently overwrite another accepted decision. Return the conflict as a blocker with affected IDs and impact. The Coordinator records only unresolved material cross-document decisions in `open-decisions.md` and sends the smallest relevant context back to the owning specialist or source owner.

Minor editorial differences that do not change behavior, ownership, contracts, controls, targets, or verification are resolved directly by the Coordinator and do not need a register entry.

## Backend-first contract, then parallel detail

When a frontend is in scope:

1. Architecture, Interface/Data, and Quality specialists establish sufficiently stable backend domain ownership, source of truth, transactions/consistency, server authorization, state/error semantics, and a versioned draft contract.
2. `frontend-design-agent` receives only relevant journeys, support commitments, backend ownership decisions, and the draft contract. It returns contract changes or confirms `None`.
3. The Coordinator records `Contract-Ready` only when applicable operations, schemas, errors, authorization context/results, idempotency/concurrency, pagination/filter/sort, limits, cancellation/deadlines, compatibility, examples, and ownership are resolved.
4. Backend and frontend detail may then proceed in parallel. A material contract change reopens only affected decisions, tasks, mocks/fixtures, contract tests, and readiness.

Do not wait for every backend deployment detail before frontend design, and do not move authoritative domain rules or security enforcement into the client for convenience.

## Authoritative write targets

- Backend SD: backend internals, architecture, domain/data/transaction ownership, server controls, runtime quality, delivery, operations, and backend verification.
- Frontend SD: frontend rendering, routing, modules, components, state/data use, experience, client quality, delivery, and frontend verification.
- Integration SD: cross-boundary ownership and behavior, contract references, authentication/session exchange, authorization context/results, errors, idempotency/concurrency, pagination/filter/sort, deadlines/cancellation/retries, compatibility, mixed versions, examples/mocks/fixtures, and contract tests.
- SD Index: source and artifact versions, routing/status, readiness, unresolved decisions, review verdict, and approvals.
- Machine-readable contract: authoritative field/protocol structure. Do not duplicate its full schema in Markdown.
- Database artifacts: authoritative affected physical model, proposed DDL, parameterized DML/query catalog, transaction/concurrency, indexes/access paths, and migration/recovery design. Backend SD owns the meaning and links the artifacts.

If artifacts disagree, the machine-readable contract owns field/protocol structure, database artifacts own affected physical schema/DDL and the critical DML/query catalog, Integration SD owns cross-boundary semantics, Backend SD owns backend/data semantics and internals, and Frontend SD owns frontend internals. The conflict blocks readiness until resolved.

## Quality gate

The Coordinator checks the assembled SD set, machine-readable contracts, source baseline, and unresolved `open-decisions.md` entries against the System Design quality gate. Record the verdict and actionable findings in the Index. Create a separate report only when audit retention is required.
