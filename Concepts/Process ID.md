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
> A process ID, or PID, is a positive integer that identifies a [[Process]] during its lifetime.

PIDs are useful for inspection, waiting, and sending [[Unix signal|signals]], but they are temporary names rather than permanent identities. After a process terminates and is reaped, the operating system may assign the same number to another process; see [[PID reuse]].

In a [[POSIX process groups|process group]], the process-group leader's PID is equal to the group's PGID.

## Related concepts

- [[Process]]
- [[PID reuse]]
- [[Process reaping]]
- [[TOCTOU race]]

