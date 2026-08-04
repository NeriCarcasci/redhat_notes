---
type: concept
status: growing
aliases:
  - backwards compatibility
  - compatibility
created: 2026-07-30
updated: 2026-07-30
tags:
  - api-design
  - releases
---

# Backward compatibility

> [!definition]
> Backward compatibility allows newer software to continue interoperating with behavior, data, or clients from an older version.

In distributed systems, deployment order is rarely perfectly synchronized. A new client may contact an old server, or an old client may contact a new server.

[Capability negotiation](Capability%20negotiation.md) and carefully bounded [Fallback behavior](Fallback%20behavior.md) support compatibility without guessing. Compatibility does not require preserving every path forever; a server can explicitly require an upgrade and return [HTTP 426 Upgrade Required](HTTP%20426%20Upgrade%20Required.md).

## Related concepts

- [Capability negotiation](Capability%20negotiation.md)
- [Fallback behavior](Fallback%20behavior.md)
- [HTTP 426 Upgrade Required](HTTP%20426%20Upgrade%20Required.md)
- [Client-server model](Client-server%20model.md)

