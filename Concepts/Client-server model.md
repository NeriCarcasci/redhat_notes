---
type: concept
status: growing
aliases:
  - client server architecture
created: 2026-07-30
updated: 2026-07-30
tags:
  - architecture
  - distributed-systems
---

# Client-server model

> [!definition]
> In the client-server model, a client initiates requests and a server provides a service across a defined protocol boundary.

Client and server may run in different processes, machines, networks, versions, and administrative domains. Their shared truth is the API contract—not shared memory or a local [Environment variable](Environment%20variable.md).

This boundary motivates [Configuration ownership](Configuration%20ownership.md), explicit [Capability negotiation](Capability%20negotiation.md), [Backward compatibility](Backward%20compatibility.md), [Authentication](Authentication.md), and [Authorization](Authorization.md).

## Related concepts

- [Configuration ownership](Configuration%20ownership.md)
- [Capability negotiation](Capability%20negotiation.md)
- [Backward compatibility](Backward%20compatibility.md)
- [Authentication](Authentication.md)
- [Authorization](Authorization.md)

