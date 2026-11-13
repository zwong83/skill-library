# Logging performance

Consider disabled-level checks, lazy formatting, serialization cost, payload size, synchronous I/O, queue capacity, backpressure, sampling, and storage/network cost. Never make request success depend on a fragile logging sink unless explicitly designed. Bound repeated events and high-cardinality fields. Measure the logging path under realistic load.

## Concrete example

Use a parameterized call such as `logger.debug("【User/Lookup】 User lookup id=%s", user_id)` instead of eagerly constructing a large string or serializing the full user object when DEBUG is disabled.
