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

It answers “are you allowed?” after [Authentication](Authentication.md) establishes identity.

When creating [Presigned URLs](Presigned%20URLs.md), the server should authorize the exact artifact operation and sign only that bounded method, path, and lifetime. [Fallback behavior](Fallback%20behavior.md) must not route around the same policy through an older endpoint.

## Related concepts

- [Authentication](Authentication.md)
- [Presigned URLs](Presigned%20URLs.md)
- [Fallback behavior](Fallback%20behavior.md)
- [Capability](Capability.md)

