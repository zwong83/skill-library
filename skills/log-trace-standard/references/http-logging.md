# HTTP logging

Log request completion at a boundary with method, route template (not raw URL), status, duration, outcome, service, and trace/request IDs. Avoid query strings, authorization headers, cookies, and full bodies unless narrowly allowlisted and redacted. Do not log the same request as an error at every layer; the owner of the failed operation should retain the exception details.

Propagate standardized trace context on outbound calls and record bounded downstream timing, status, and retry information.

## Concrete example

```json
{"event":"http.request.completed","message":"【Payments/HTTP】 Request completed","method":"POST","route":"/payments","status":201,"duration_ms":142,"trace_id":"T1"}
```
