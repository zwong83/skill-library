# CDN Caching

## Eligibility, keys, and variants

- Identify the routes that may be shared at the edge. Bypass shared caching for personalized or authenticated responses unless an explicit, verified contract permits sharing and isolates all relevant variants.
- Build the cache key from the host, path, and relevant query parameters, headers, or cookies that affect the response. Verify the provider's normalization and `Vary` support. Keep inputs that change the response in the cache key or bypass caching for those requests. Forwarding an input to the origin does not guarantee it is in the key.
- Avoid unnecessary high-cardinality key inputs that reduce hit rate. Verify that tenant, locale, and representation boundaries are preserved. Test two distinct users or variants against a warmed cache when isolation is material.

## Edge freshness and origin protection

- Set the edge and browser lifetimes independently where required. Use shared-cache directives such as `s-maxage` only where supported, and check CDN overrides, minimum TTL, and the handling of `private` and `no-store`. Evaluate error caching separately from successful responses.
- Define whether stale content may be served during revalidation or origin failure. Cap the allowed stale window and verify the provider's behavior. Consider request coalescing, an origin shield, or bounded warmup where available if miss bursts could overload the origin.

## Invalidation and verification

- Prefer versioned URLs for immutable assets. For mutable responses, define purge ownership, exact scope, treatment of variants, and how to verify propagation. Account for browser freshness independently.
- Inspect CDN cache status, `Age`, origin response headers, hit rate, and origin requests. Test first miss, repeat hit, variant separation, expiry, purge, and origin failure as required. Use the deployed provider's documentation for key construction, header precedence, purge, and stale behavior. [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html) · [CloudFront cache key example](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/controlling-the-cache-key.html)
