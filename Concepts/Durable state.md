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

Durability is one part of [Crash consistency](Crash%20consistency.md). An incomplete marker is useful only if its persistence ordering is strong enough for the failure model being handled.

## Related concepts

- [Crash consistency](Crash%20consistency.md)
- [Atomic filesystem operation](Atomic%20filesystem%20operation.md)
- [File locking](File%20locking.md)
- [Idempotent setup](Idempotent%20setup.md)

