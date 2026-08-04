---
type: concept
status: growing
aliases:
  - mutex
  - critical section
created: 2026-07-30
updated: 2026-07-30
tags:
  - concurrency
---

# Mutual exclusion

> [!definition]
> Mutual exclusion ensures that at most one participating actor executes a protected critical section at a time.

A thread lock coordinates threads that share a process. [File locking](File%20locking.md) can coordinate cooperating processes. Mutual exclusion can protect state transitions and reduce a [Race condition](Race%20condition.md), but the protected region must include the whole invariant—not merely one convenient line.

Locks do not automatically provide [Crash consistency](Crash%20consistency.md), [Idempotency](Idempotency.md), fairness, or freedom from deadlock.

## Related concepts

- [Race condition](Race%20condition.md)
- [File locking](File%20locking.md)
- [Linearization point](Linearization%20point.md)
- [Idempotency](Idempotency.md)
- [Crash consistency](Crash%20consistency.md)

