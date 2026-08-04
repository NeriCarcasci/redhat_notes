---
type: concept
status: growing
aliases:
  - environment variables
  - env var
created: 2026-07-30
updated: 2026-07-30
tags:
  - configuration
  - operating-systems
---

# Environment variable

> [!definition]
> An environment variable is a string-valued key inherited by a [[Process]] from its parent environment.

Because every value is text, parsing matters: the non-empty string `"false"` is truthy under `bool("false")`, but a configuration parser should interpret it as Boolean false.

Environment variables are local to a process environment. They do not automatically cross a [[Client-server model|client-server]] boundary, which makes [[Configuration ownership]] essential.

Do not place secrets in logs, exception messages, or child environments without considering exposure.

## Related concepts

- [[Process]]
- [[Child process]]
- [[Configuration ownership]]
- [[Client-server model]]

