# Sampling, Cost, and Data Control

## Sampling

- Define the investigation and retention objective before choosing a policy.
- Head sampling decides early and can use only information available at that point.
- Tail sampling can retain traces based on completed outcomes but adds collector/state cost and delay.
- Preserve diagnostically important failures, high latency, and rare workflows according to policy without assuming every error is safe to retain.
- Keep parent-based decisions coherent across services and document behavior for remote unsampled parents.
- Add known span links at span creation when they may affect sampling. A normal parent-based sampler may ignore links, especially when a batch consumer starts a new root span; select and test a link-aware policy or tail sampling when retaining producer-linked work is required.
- Test sampling configuration and upgrades; do not infer collection merely because a span is recording locally.

## Cost and performance

- Avoid redundant manual spans already produced by auto-instrumentation.
- Bound attribute count/size, links, events, and baggage.
- Avoid expensive attribute computation when the span is not recording.
- Estimate spans per request/job, throughput, export queue, collector capacity, retention, and backend cost.
- Define exporter failure, queue saturation, drop, retry, and shutdown/flush behavior without blocking critical paths unexpectedly.

## Privacy and security

Apply the same exclusions as logs. Do not record secrets, credentials, raw payloads, sensitive personal data, or unrestricted user input. Sampling is not a privacy control: unsampled or partially exported telemetry may still be processed locally or by intermediate components.
