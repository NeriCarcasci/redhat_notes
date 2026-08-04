---
type: concept
status: growing
aliases:
  - process session
  - session ID
  - SID
created: 2026-07-30
updated: 2026-07-30
tags:
  - operating-systems
---

# POSIX session

> [!definition]
> A POSIX session is a collection of one or more [process groups](POSIX%20process%20groups.md), traditionally associated with terminal job control.

A session has a leader whose [Process ID](Process%20ID.md) is the session ID. Calling `setsid()` creates a new session and a new process group, detaching the caller from its former session.

Python's `subprocess.Popen(..., start_new_session=True)` requests this behavior in the child before program execution. Executors use it to isolate a job group that can later receive a group-wide [Unix signal](Unix%20signal.md).

## Related concepts

- [POSIX process groups](POSIX%20process%20groups.md)
- [Process ID](Process%20ID.md)
- [Unix signal](Unix%20signal.md)

