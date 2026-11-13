# Logging code review

- [ ] Event is meaningful and stable
- [ ] Message follows the project format, including `【Service/Operation】` where required
- [ ] Severity reflects operational meaning
- [ ] Structured fields are searchable and bounded
- [ ] Trace/request context is present or intentionally unavailable
- [ ] Exception and causal chain are preserved where needed
- [ ] No sensitive data or unsafe payload logging
- [ ] No duplicate or high-volume noise
- [ ] Existing framework and conventions are reused
- [ ] Formatting and serialization are lazy/appropriate

## Concrete example

For a payment error review, confirm the event is `payment.failed`, severity is `ERROR`, `payment_id` is present, the exception is attached once, and tokens or card data are absent.
