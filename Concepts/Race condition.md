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

Common forms include [Cancellation races](Cancellation%20races.md) and [time-of-check/time-of-use races](TOCTOU%20race.md). Typical tools include [Mutual exclusion](Mutual%20exclusion.md), immutable state, message passing, atomic operations, and state machines with a clear [Linearization point](Linearization%20point.md).

Tests for races should coordinate meaningful event boundaries rather than rely only on arbitrary sleeps.

## Related concepts

- [Cancellation races](Cancellation%20races.md)
- [TOCTOU race](TOCTOU%20race.md)
- [Mutual exclusion](Mutual%20exclusion.md)
- [Linearization point](Linearization%20point.md)

