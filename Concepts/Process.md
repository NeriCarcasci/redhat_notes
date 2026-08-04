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

One program can have many processes. Each has a [[Process ID]], may create a [[Child process]], belongs to a [[POSIX process groups|process group]], and responds to [[Unix signal|signals]] according to the operating system and program.

A process can contain multiple threads. Threads share the process's memory and resources; separate processes normally do not.

The process lifetime is not quite finished when its code exits: on POSIX, its parent still performs [[Process reaping]] to collect the exit status.

## Related concepts

- [[Process ID]]
- [[Child process]]
- [[POSIX process groups]]
- [[POSIX session]]
- [[Process reaping]]

