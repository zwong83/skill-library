# Java

Prefer the project's existing SLF4J facade and configured Logback or Log4j2 backend. Use MDC or the framework's context integration for request and trace fields; verify cleanup across thread pools. In Spring Boot, inspect `logback-spring.xml`/application configuration and OpenTelemetry instrumentation before adding manual propagation. Use parameterized/lazy logging and async appenders only with bounded queues and a defined loss policy.

## Concrete example

```java
log.info("【Payment/Create】 Payment created payment_id={} provider={}", paymentId, provider);
```
