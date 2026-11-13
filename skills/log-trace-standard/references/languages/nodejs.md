# Node.js

Reuse the project's Pino, Winston, or established logger. Use `AsyncLocalStorage` or framework integrations for request context and verify propagation across promises, workers, and queues. Prefer structured JSON, serializers with allowlists, and bounded error/request fields. Avoid synchronous transports in hot paths.

## Concrete example

```js
logger.info({ event: 'payment.created', payment_id: paymentId }, '【Payment/Create】 Payment created');
```
