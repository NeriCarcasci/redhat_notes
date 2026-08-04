---
type: concept
status: growing
aliases:
  - POSIX signal
  - signals
created: 2026-07-30
updated: 2026-07-30
tags:
  - operating-systems
---

# Unix signal

> [!definition]
> A Unix signal is an asynchronous notification delivered to a [[Process]] or [[POSIX process groups|process group]].

Signals represent events such as interruption, termination, or an invalid memory access. A process may handle, ignore, or receive the default action for many signals. `SIGKILL` cannot be caught or ignored, which makes it effective but prevents in-process cleanup.

Termination and [[Process reaping]] are separate: after a signal makes a child exit, its parent still collects the exit status.

## Related concepts

- [[Process]]
- [[POSIX process groups]]
- [[Cancellation races]]
- [[Process reaping]]
- [[Crash consistency]]

