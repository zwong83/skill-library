# OpenSpec CLI Bootstrap Gate

Use this reference before any OpenSpec project command when CLI availability, installation, version, PATH, or compatibility is unknown.

## State model

Distinguish these states:

| State | Meaning |
|---|---|
| `CLI Unavailable` | No executable can be resolved or executed. |
| `CLI Installed-Unverified` | An executable exists, but version or integrity/source is not sufficiently known for the requested workflow. |
| `CLI Ready` | The executable and local version are verified and compatible with applicable project constraints. |
| `Project Uninitialized` | The CLI is ready, but the target project has no valid OpenSpec context. |
| `Project Initialized` | The CLI is ready and the project context can be read successfully. |

Installing the CLI does not initialize a project. Initializing a project does not authorize proposal creation or implementation.

## 1. Detect without mutation

Resolve the executable using the environment's normal command lookup. Obtain the local version without an online update check:

```bash
openspec version --json
```

Use structured output only when it is valid JSON with the expected fields. Older versions may not support this form; fall back to:

```bash
openspec --version
```

Record the resolved executable, version, install method/scope when discoverable, and applicable project version constraint. Do not claim a version, install source, or compatibility result that was not observed.

## 2. Select an installation path

When the CLI is unavailable or incompatible, use this precedence:

1. explicit project or organization instructions and pinned version;
2. the current official [OpenSpec installation documentation](https://github.com/Fission-AI/OpenSpec/blob/main/docs/installation.md);
3. another installation method explicitly approved by the user or environment owner.

Official installation options may include the standalone OpenSpec binary installer and the official `@fission-ai/openspec` package through a supported package manager. Verify current official documentation at execution time because commands, prerequisites, and supported scopes can change.

Do not silently choose global, user, project-local, temporary, source-checkout, or standalone scope. Prefer the project's established method and pinned version when present. Do not use third-party mirrors or packages merely because their names look similar.

## 3. Installation authorization gate

Before installation or upgrade, present:

- official/project-approved source;
- proposed version or update channel;
- installation method and scope;
- target path when known;
- runtime/package-manager prerequisites;
- expected network access and checksum/signature verification;
- PATH or shell-configuration impact;
- uninstall/rollback approach.

Obtain the authorization required by the active environment immediately before executing the install. A request to run SDD does not by itself authorize global/user package installation, remote installer execution, PATH changes, shell-profile edits, or an upgrade of an existing CLI.

## 4. Verify after installation

After an authorized install:

1. resolve which `openspec` executable the shell will run;
2. verify the local version without an update check;
3. confirm the installed version satisfies applicable project constraints;
4. run a non-mutating help/version command to confirm execution;
5. report PATH ambiguity or multiple-install shadowing instead of guessing;
6. record the observed source/method/scope and version.

If the executable is still unavailable, incompatible, or shadowed by another installation, return `Blocked: OpenSpec CLI unavailable or incompatible` with exact evidence. Do not proceed to project initialization.

## 5. Project initialization boundary

Only after the CLI is `CLI Ready` may the workflow inspect project context. If the project is uninitialized:

- complete the SDD source-readiness gate first;
- identify the intended project root, schema, language/tool integration, and files expected to be written;
- obtain separate authorization for `openspec init`;
- run initialization from the intended project root;
- re-read project state and report the active schema from actual CLI output.

Do not treat installation approval as project-initialization approval, and do not treat initialization approval as permission to create a change or modify production code.
