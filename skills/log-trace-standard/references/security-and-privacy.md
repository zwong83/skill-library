# Logging Security and Privacy

## Exclude by default

- passwords, PINs, secret answers, private keys, encryption material;
- access/refresh tokens, API keys, authorization headers, cookies, and raw session identifiers;
- database connection strings and credentials;
- raw payment-card, bank, health, government-identifier, biometric, or other sensitive personal data;
- complete request/response bodies, uploaded file contents, prompts/model outputs, or arbitrary serialized objects;
- data classified above the logging system's permitted level.

Masking, hashing, pseudonymization, or encryption is allowed only when the approved policy and operational use justify it. A hashed secret may still be sensitive and linkable.

## Untrusted input

- Sanitize carriage returns, line feeds, delimiters, terminal escapes, and control characters.
- Use structured parameters rather than concatenating untrusted values into templates.
- Bound length and normalize encoding.
- Preserve the security event even if one unsafe field must be omitted or replaced.

## HTTP and API allowlist

Use a positive allowlist for HTTP/API fields. Do not log all headers, raw URL query strings/fragments, `multipart/form-data`, cookies, authorization headers, unreviewed custom headers, complete bodies, or raw exception messages that may embed request data. Prefer method, route template, approved response status/outcome, stable error classification, bounded timing/size, trace context, and explicitly approved pseudonymous identifiers.

## Security/audit events

Consider authentication/authorization failures, validation failures, privileged changes, sensitive-data access, administrative actions, key/configuration changes, suspicious business-flow violations, startup/shutdown, and security-control failures according to policy. Do not infer that every event is malicious; record outcome and context for correlation.

## Protection and lifecycle

Define who can emit, read, export, modify, and delete logs; integrity controls; retention/deletion; environment separation; backup; incident access; and legal/privacy constraints. Logging configuration changes should follow change control, and required security/audit logging should not be silently disabled.

Basis: [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html).
