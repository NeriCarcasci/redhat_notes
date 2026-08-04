---
type: concept
status: growing
aliases:
  - content length
  - file size metadata
created: 2026-07-30
updated: 2026-07-30
tags:
  - http
---

# Content-Length

> [!definition]
> `Content-Length` is an HTTP field that states the size, in bytes, of the associated message content when that size is known and the field is applicable.

It supports progress reporting, capacity planning, and some truncation checks. It is not universally present, and a [streaming download](Streaming%20HTTP%20downloads.md) can often read until the protocol marks the response complete.

Application metadata named `file_size` may be related but is not automatically identical to the HTTP field.

## Related concepts

- [Streaming HTTP downloads](Streaming%20HTTP%20downloads.md)
- [Backpressure](Backpressure.md)
- [HTTP status code](HTTP%20status%20code.md)

