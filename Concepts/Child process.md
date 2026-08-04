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
> A child process is a [[Process]] created by another process, called its parent.

The child receives a new [[Process ID]] and initially inherits selected state such as environment variables, open descriptors, and its parent's [[POSIX process groups|process group]]. The exact inherited state depends on the creation API and operating system.

In Python, `subprocess.Popen(...)` creates and represents a child. The parent is responsible for [[Process reaping|reaping]] that direct child, even if the child creates descendants of its own.

## Related concepts

- [[Process]]
- [[Process ID]]
- [[Process reaping]]
- [[Environment variable]]
- [[POSIX process groups]]

