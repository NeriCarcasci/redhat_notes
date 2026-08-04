---
type: concept
status: growing
aliases:
  - access control
created: 2026-07-30
updated: 2026-07-30
tags:
  - security
---

# Authorization

> [!definition]
> Authorization decides whether an authenticated principal may perform a particular action on a resource.

It answers “are you allowed?” after [[Authentication]] establishes identity.

When creating [[Presigned URLs]], the server should authorize the exact artifact operation and sign only that bounded method, path, and lifetime. [[Fallback behavior]] must not route around the same policy through an older endpoint.

## Related concepts

- [[Authentication]]
- [[Presigned URLs]]
- [[Fallback behavior]]
- [[Capability]]

