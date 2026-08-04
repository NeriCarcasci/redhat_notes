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

A thread lock coordinates threads that share a process. [[File locking]] can coordinate cooperating processes. Mutual exclusion can protect state transitions and reduce a [[Race condition]], but the protected region must include the whole invariant—not merely one convenient line.

Locks do not automatically provide [[Crash consistency]], [[Idempotency]], fairness, or freedom from deadlock.

## Related concepts

- [[Race condition]]
- [[File locking]]
- [[Linearization point]]
- [[Idempotency]]
- [[Crash consistency]]

