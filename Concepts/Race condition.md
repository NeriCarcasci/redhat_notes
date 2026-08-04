---
type: concept
status: growing
aliases:
  - race
created: 2026-07-30
updated: 2026-07-30
tags:
  - concurrency
---

# Race condition

> [!definition]
> A race condition exists when correctness depends on the timing or ordering of concurrent events.

The problem is not simply that operations overlap; it is that different valid schedules produce different, sometimes invalid, outcomes.

Common forms include [[Cancellation races]] and [[TOCTOU race|time-of-check/time-of-use races]]. Typical tools include [[Mutual exclusion]], immutable state, message passing, atomic operations, and state machines with a clear [[Linearization point]].

Tests for races should coordinate meaningful event boundaries rather than rely only on arbitrary sleeps.

## Related concepts

- [[Cancellation races]]
- [[TOCTOU race]]
- [[Mutual exclusion]]
- [[Linearization point]]

