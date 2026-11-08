# Security Verification Matrix

| Control area | Representative safe evidence |
|---|---|
| Authentication/session | valid/invalid/expired/revoked flows, fixation/rotation/logout behavior, safe errors and audit |
| Authorization/isolation | allowed and denied subject-action-resource cases, object/tenant/field isolation, forbidden effects |
| Input/output | boundary/malformed inputs, parameterized interfaces, destination encoding, limits, safe failures |
| Sensitive data/crypto | approved algorithm/library/configuration, transport/storage protection, key/secret lifecycle evidence, no plaintext fallback |
| Audit/privacy | required events, actor/context/result, integrity/access/retention, redaction and minimization |
| Dependencies/supply chain | inventory, supported versions, vulnerability/signature/provenance policy, exception/patch ownership |
| Configuration/runtime | secure defaults, environment separation, exposed surfaces, headers/policies, failure behavior, drift |
| Abuse/availability | approved throttling, quotas, duplicate/replay controls, bounded resource use, detection/response evidence |

For each case record threat/control IDs, target and enforcement point, actor/security context, positive or negative category, exact non-destructive action, expected result and forbidden side effects, required audit/detection, rate/stop limits, technique/tool, evidence, finding/disposition, and owner.
