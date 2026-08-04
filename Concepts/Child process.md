---
type: concept
status: growing
aliases:
  - subprocess
  - child
created: 2026-07-30
updated: 2026-07-30
tags:
  - operating-systems
---

# Child process

> [!definition]
> A child process is a [Process](Process.md) created by another process, called its parent.

The child receives a new [Process ID](Process%20ID.md) and initially inherits selected state such as environment variables, open descriptors, and its parent's [process group](POSIX%20process%20groups.md). The exact inherited state depends on the creation API and operating system.

In Python, `subprocess.Popen(...)` creates and represents a child. The parent is responsible for [reaping](Process%20reaping.md) that direct child, even if the child creates descendants of its own.

## Related concepts

- [Process](Process.md)
- [Process ID](Process%20ID.md)
- [Process reaping](Process%20reaping.md)
- [Environment variable](Environment%20variable.md)
- [POSIX process groups](POSIX%20process%20groups.md)

