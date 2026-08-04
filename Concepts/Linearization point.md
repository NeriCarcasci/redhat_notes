---
type: concept
status: growing
aliases:
  - linearization
created: 2026-07-30
updated: 2026-07-30
tags:
  - concurrency
  - distributed-systems
---

# Linearization point

> [!definition]
> A linearization point is the conceptual instant during a concurrent operation when its effect becomes committed and visible as if operations occurred one at a time.

It may be a lock-protected assignment, successful compare-and-swap, database commit, or accepted message. Before that point the operation can lose a [[Race condition]]; after it, other actors must respect the result.

For [[Cancellation races]], the linearization point determines whether completion or cancellation owns the terminal state.

## Related concepts

- [[Race condition]]
- [[Cancellation races]]
- [[Mutual exclusion]]
- [[Atomic filesystem operation]]

