---
type: concept
status: growing
aliases:
  - HTTP response status
created: 2026-07-30
updated: 2026-07-30
tags:
  - http
---

# HTTP status code

> [!definition]
> An HTTP status code is a three-digit response code describing the result of an HTTP request.

The first digit identifies the class: informational `1xx`, successful `2xx`, redirection `3xx`, client error `4xx`, or server error `5xx`.

A status is part of a protocol contract. Choose it for semantics, not merely because its English phrase sounds convenient. A structured response body should add actionable detail. See [[HTTP 426 Upgrade Required]] for an upgrade-specific example.

## Related concepts

- [[HTTP 426 Upgrade Required]]
- [[Fallback behavior]]
- [[Backward compatibility]]
- [[Streaming HTTP downloads]]

