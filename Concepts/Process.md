---
type: concept
status: growing
aliases:
  - operating-system process
created: 2026-07-30
updated: 2026-07-30
tags:
  - operating-systems
---

# Process

> [!definition]
> A process is a running program instance together with its address space, open resources, execution state, and operating-system identity.

One program can have many processes. Each has a [Process ID](Process%20ID.md), may create a [Child process](Child%20process.md), belongs to a [process group](POSIX%20process%20groups.md), and responds to [signals](Unix%20signal.md) according to the operating system and program.

A process can contain multiple threads. Threads share the process's memory and resources; separate processes normally do not.

The process lifetime is not quite finished when its code exits: on POSIX, its parent still performs [Process reaping](Process%20reaping.md) to collect the exit status.

## Related concepts

- [Process ID](Process%20ID.md)
- [Child process](Child%20process.md)
- [POSIX process groups](POSIX%20process%20groups.md)
- [POSIX session](POSIX%20session.md)
- [Process reaping](Process%20reaping.md)

