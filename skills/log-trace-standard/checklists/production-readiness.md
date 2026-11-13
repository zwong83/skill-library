# Production readiness

- [ ] Output destination and collector behavior are defined
- [ ] Environment-specific levels and sampling are configured
- [ ] Rotation, retention, permissions, and disk-full behavior are defined when files are used
- [ ] Context propagates across relevant HTTP, MQ, and async boundaries
- [ ] Redaction is tested for messages, exceptions, requests, and forwarded logs
- [ ] Volume, latency, queue limits, loss policy, and shutdown flushing are understood
- [ ] Schema and dashboards/search queries are compatible

## Concrete example

For a containerized service, verify JSON logs go to stdout, the collector receives `trace_id`, production defaults to INFO, and a disk rotation test is not required because the app does not write local files.
