---
type: concept
status: growing
aliases:
  - authenticating identity
created: 2026-07-30
updated: 2026-07-30
tags:
  - security
---

# Authentication

> [!definition]
> Authentication establishes or verifies the identity of a user, service, or other principal.

It answers “who are you?” [[Authorization]] then answers “what may you do?”

In a [[Presigned URLs|presigned URL]] flow, the application server authenticates the requester before creating a bounded signed request. The object store later authenticates that signed request without receiving the user's long-lived storage credentials.

## Related concepts

- [[Authorization]]
- [[Presigned URLs]]
- [[Client-server model]]

