# Log-writing style

Write a stable event that says what happened and attaches searchable fields. Include the `【Service/Operation】` prefix where the project uses or requires it. Prefer `【Payment/Create】 Payment creation failed` with `payment_id`, `error_code`, and `provider`; avoid `Something went wrong`, `Entering method`, `Reached here`, and concatenated unlabelled values.

Use consistent tense, names, and field types. Do not embed volatile identifiers in the event name. Keep messages understandable without source-code knowledge and avoid logging the same event again at every layer.

## Concrete example

```text
Good: 【Payment/Create】 Payment creation failed {payment_id=P123, provider=stripe, error_code=PAYMENT_TIMEOUT}
Bad: Something went wrong while calling createPayment(P123)
```
