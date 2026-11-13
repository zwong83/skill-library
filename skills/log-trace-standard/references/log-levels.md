# Log levels

Use the least severe level that preserves operational meaning:

| Level | Use |
|---|---|
| TRACE | Extremely detailed diagnostics; normally off in production |
| DEBUG | Developer diagnostics useful during investigation |
| INFO | Meaningful normal lifecycle or business behavior |
| WARN | Abnormal, recoverable behavior or a degraded fallback |
| ERROR | An operation failed or data could not be processed |
| FATAL | The process cannot reasonably continue, where supported |

Do not use WARN merely because something is noteworthy, or ERROR for every exception. A cache miss is usually DEBUG; a cache outage with database fallback is WARN; a failed payment is ERROR. Alerting should use impact, rates, and thresholds rather than severity alone.

## Concrete example

```text
DEBUG 【User/Lookup】 Cache miss key=user:42
WARN 【Cache/Fallback】 Cache unavailable fallback=database
ERROR 【Payment/Create】 Payment failed payment_id=P123 error_code=PAYMENT_TIMEOUT
```
