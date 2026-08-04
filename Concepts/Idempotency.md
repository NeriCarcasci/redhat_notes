---
type: concept
status: growing
aliases:
  - idempotent operation
created: 2026-07-30
updated: 2026-07-30
tags:
  - reliability
  - api-design
---

# Idempotency

> [!definition]
> An operation is idempotent when applying it more than once has the same intended effect as applying it once.

Mathematically: `f(f(x)) = f(x)`.

“Set status to canceled” can be idempotent; “increment cancellation counter” is not. Idempotency is valuable when a caller cannot tell whether an earlier attempt succeeded and must retry.

It does not mean the operation runs only once, has no cost, or is protected from concurrent execution. [[Idempotent setup]] often also needs [[Mutual exclusion]] and [[Crash consistency]].

## Related concepts

- [[Idempotent setup]]
- [[Mutual exclusion]]
- [[Crash consistency]]
- [[Fallback behavior]]

