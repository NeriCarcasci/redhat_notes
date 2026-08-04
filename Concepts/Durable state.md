---
type: concept
status: growing
aliases:
  - persistence
  - durable storage
created: 2026-07-30
updated: 2026-07-30
tags:
  - storage
  - reliability
---

# Durable state

> [!definition]
> Durable state is information expected to survive process termination and, at the promised level, machine or storage failure.

Writing through a language API may update only memory or an operating-system cache. Stronger guarantees can require flushing file contents and directory metadata, a database commit, replication, or a storage-specific acknowledgement.

Durability is one part of [[Crash consistency]]. An incomplete marker is useful only if its persistence ordering is strong enough for the failure model being handled.

## Related concepts

- [[Crash consistency]]
- [[Atomic filesystem operation]]
- [[File locking]]
- [[Idempotent setup]]

