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

[[Capability negotiation]] and carefully bounded [[Fallback behavior]] support compatibility without guessing. Compatibility does not require preserving every path forever; a server can explicitly require an upgrade and return [[HTTP 426 Upgrade Required]].

## Related concepts

- [[Capability negotiation]]
- [[Fallback behavior]]
- [[HTTP 426 Upgrade Required]]
- [[Client-server model]]

