# C++

Reuse the project's established library such as spdlog, Boost.Log, or a platform logger. Use structured fields or a stable formatter, explicit severity filtering, and RAII-safe context handling. Bound formatting and asynchronous queues, define thread/process behavior, and verify rotation and shutdown flushing.

## Concrete example

```cpp
spdlog::info("【Payment/Create】 Payment created payment_id={}", payment_id);
```
