# Authorization, Evidence, and Verdicts

## Authorization record

Capture target identifiers, owner, environment, permitted techniques/tools, accounts/roles/tenants, time window, source ranges when relevant, rate/concurrency, test data, prohibited actions, stop conditions, monitoring, incident contact, cleanup, and evidence access/retention. Absence of a restriction is not permission.

## Evidence

Retain the minimum reproducible evidence: target revision/configuration, tool/version/ruleset, sanitized request/input, response/outcome, authoritative state and forbidden-effect check, audit/detection record, timestamps/correlation, system health, finding validation, and retest. Remove credentials, tokens, keys, personal data, internal topology, and unnecessary exploit detail.

## Verdicts

- `Security-Passed`: every required authorized control case passed, required findings are resolved/accepted by the authorized owner, and limitations are outside the claimed scope.
- `Security-Failed`: a required control failed or an unresolved finding violates the approved release gate.
- `Security-Blocked`: required authorization, target, environment, identity/data, tooling, safe execution, or trustworthy evidence is unavailable.

Do not convert blocked, prohibited, skipped, rate-limited, inconclusive, or scanner-only evidence into a pass.
