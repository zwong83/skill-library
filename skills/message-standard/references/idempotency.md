# Message Idempotency

Use a stable idempotency key, check or reserve it at the correct transaction boundary, apply the business effect, and record completion. A database uniqueness constraint or durable processed-message table is usually safer for durable business effects than an ephemeral deduplication cache.

Define the result for a duplicate, an in-flight retry, a partially completed external call, and an expired deduplication record. Idempotency must cover the actual side effect, not only the broker acknowledgement.
