# Browser Caching

## Freshness and validation

- For the browser HTTP cache, set `Cache-Control` based on how long the response may be reused without contacting the server. `no-cache` allows storage but requires successful validation before reuse. `no-store` tells caches not to store the response.
- Use `ETag` or `Last-Modified` when the browser should validate a stored response. Verify the conditional request path and the headers on a `304 Not Modified` response.
- Give fingerprinted assets a long freshness lifetime when the URL changes with the content. Set a shorter lifetime or require revalidation for the HTML or manifest that points to those assets. An edge purge cannot recall fresh copies in browser caches.

## Response variants and private data

- Set `Vary` for request headers that change the representation, such as language or encoding. Avoid unnecessary variants. Check that any shared cache in the path also handles the intended variants.
- Use `private` to prevent shared caches from storing a response that may be stored in a user's browser. Use `no-store` when storage itself is unacceptable. Assess actual response data, including account changes, logout, and use of a shared device.

## Service worker caching

If a service worker uses Cache Storage, verify its fetch strategy, cache naming and versioning, cleanup of obsolete entries, and offline fallback. Its stored responses and reuse rules are managed by the application. Changing HTTP cache headers alone does not update that strategy or clear stored entries. [Service Workers Cache interface](https://www.w3.org/TR/service-workers/#cache-interface)

## Verification

Inspect the response headers, network request and status, and whether the browser served the response from its HTTP cache or a service worker. Reproduce the actual navigation or reload flow. For a deploy issue, check the document's asset URLs and whether old and new clients can both fetch the versions they reference. [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html)
