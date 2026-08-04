---
type: concept
status: growing
aliases:
  - PID
created: 2026-07-30
updated: 2026-07-30
tags:
  - operating-systems
---

# Process ID

> [!definition]
> A process ID, or PID, is a positive integer that identifies a [Process](Process.md) during its lifetime.

PIDs are useful for inspection, waiting, and sending [signals](Unix%20signal.md), but they are temporary names rather than permanent identities. After a process terminates and is reaped, the operating system may assign the same number to another process; see [PID reuse](PID%20reuse.md).

In a [process group](POSIX%20process%20groups.md), the process-group leader's PID is equal to the group's PGID.

## Related concepts

- [Process](Process.md)
- [PID reuse](PID%20reuse.md)
- [Process reaping](Process%20reaping.md)
- [TOCTOU race](TOCTOU%20race.md)

