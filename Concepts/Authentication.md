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

It answers “who are you?” [Authorization](Authorization.md) then answers “what may you do?”

In a [presigned URL](Presigned%20URLs.md) flow, the application server authenticates the requester before creating a bounded signed request. The object store later authenticates that signed request without receiving the user's long-lived storage credentials.

## Related concepts

- [Authorization](Authorization.md)
- [Presigned URLs](Presigned%20URLs.md)
- [Client-server model](Client-server%20model.md)

