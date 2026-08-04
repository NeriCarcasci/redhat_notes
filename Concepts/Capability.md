---
type: concept
status: growing
aliases:
  - supported capability
created: 2026-07-30
updated: 2026-07-30
tags:
  - api-design
  - architecture
---

# Capability

> [!definition]
> A capability is an operation or behavior that a component is able—and, in context, permitted—to provide.

Examples include “can generate presigned downloads” and “requires clients to avoid legacy artifact proxy routes.” The first is descriptive support; the second also expresses policy. Keeping those meanings explicit prevents ambiguous [Fallback behavior](Fallback%20behavior.md).

Capabilities can be static configuration, implementation traits, or runtime observations. In a [Client-server model](Client-server%20model.md), they are commonly exposed through [Capability negotiation](Capability%20negotiation.md).

## Related concepts

- [Capability negotiation](Capability%20negotiation.md)
- [Fail-fast validation](Fail-fast%20validation.md)
- [Fallback behavior](Fallback%20behavior.md)
- [Configuration ownership](Configuration%20ownership.md)

