---
type: concept
status: growing
aliases:
  - time-of-check time-of-use race
  - TOCTOU
created: 2026-07-30
updated: 2026-07-30
tags:
  - concurrency
  - security
---

# TOCTOU race

> [!definition]
> A time-of-check/time-of-use race occurs when code checks a fact and later acts on it after another actor may have changed the underlying state.

```text
check(resource)
    ← another actor changes resource
use(resource)
```

Examples include checking a path before opening it or checking a [[Process ID]] before signaling it after [[PID reuse]]. Prefer an atomic operation, stable handle, or [[Mutual exclusion]] that covers both validation and use.

## Related concepts

- [[Race condition]]
- [[PID reuse]]
- [[Atomic filesystem operation]]
- [[Mutual exclusion]]

