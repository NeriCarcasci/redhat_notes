---
type: concept
status: growing
aliases:
  - atomic rename
  - atomic file operation
created: 2026-07-30
updated: 2026-07-30
tags:
  - filesystems
  - concurrency
---

# Atomic filesystem operation

> [!definition]
> An atomic filesystem operation appears to observers as one indivisible change: they see the state before it or after it, not a partial intermediate step.

Renaming a file within the same filesystem is commonly used to publish completed content:

1. write a temporary file;
2. flush and close it as required;
3. rename it over the destination.

Atomic visibility does not necessarily mean [[Durable state|durability]] after a crash. Filesystem, mount, and platform semantics still matter.

This pattern helps [[Crash consistency]] and [[Streaming HTTP downloads]], but cannot safely relocate resources that embed absolute paths.

## Related concepts

- [[Crash consistency]]
- [[Durable state]]
- [[TOCTOU race]]
- [[Streaming HTTP downloads]]

