# Schema, Loading, and Change

## Configuration Contract

For each key record:

- stable name, purpose, owner, and consumers;
- type, format, units, allowed values/range, and cross-field constraints;
- required/optional status and whether a default is safe;
- source, scope, precedence, environment, tenant, and region behavior;
- sensitivity and whether the value may appear in diagnostics;
- startup-only or dynamic behavior, propagation target, and stale tolerance;
- compatibility window, deprecation date, and replacement key;
- change risk, approval, tests, rollback, and audit evidence.

Reject unknown keys when safety benefits outweigh forward-compatibility needs; otherwise surface them as warnings. Never coerce malformed security- or money-sensitive values silently.

## Loading and Precedence

Define an explicit order such as defaults, packaged non-sensitive baseline, environment configuration, external provider, then authorized runtime override. The exact order is project-specific, but it must be deterministic and tested.

- Resolve the effective configuration before readiness whenever possible.
- Expose key names, source/version, and validation status without exposing sensitive values.
- Avoid reading mutable global environment state throughout business code; bind at a controlled composition boundary.
- Keep the same application artifact promotable across environments by injecting environment-specific configuration outside the artifact.

## Dynamic Refresh

Define whether changes are atomic as a snapshot or independent by key. State polling/watch behavior, propagation delay, ordering, version checks, stale reads, missed events, reconnect, and concurrent update behavior.

Validate a candidate snapshot before activation. Preserve the last known safe version only when stale operation is explicitly acceptable. For unsafe or incompatible changes, reject activation and alert rather than partially applying values.

## Change Lifecycle

1. Propose a versioned change with owner, reason, affected consumers, and risk.
2. Validate schema, semantics, compatibility, and security.
3. Exercise the change in a representative lower environment.
4. Roll out progressively where impact warrants it.
5. Observe defined success and guardrail signals.
6. Roll back or roll forward using a tested procedure.
7. Reconcile drift and remove obsolete keys after the compatibility window.

Do not claim rollback is safe if old code cannot consume the restored configuration or if a data/schema change is irreversible.

## Primary References

- [Kubernetes Configuration](https://kubernetes.io/docs/concepts/configuration/)
- [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
