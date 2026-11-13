# Files, rotation, and retention

Use stdout/stderr with a platform collector in containers unless a file is a stated requirement. For file logging, define location, permissions, format, size/time rotation, compression, retention, startup behavior, disk-full behavior, and collection handoff. Ensure multiple processes do not corrupt or independently rotate the same file unless the framework supports it.

Retention should follow operational, legal, and cost requirements; do not keep sensitive logs longer than necessary.

## Concrete example

For a VM-based service, rotate `app.log` daily and at 100 MB, retain 14 compressed files, restrict access to the service account and operators, and alert before the disk reaches its capacity threshold.
