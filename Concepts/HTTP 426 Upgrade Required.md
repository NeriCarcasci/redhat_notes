---
type: concept
status: growing
aliases:
  - 426 Upgrade Required
created: 2026-07-30
updated: 2026-07-30
tags:
  - http
  - api-design
---

# HTTP 426 Upgrade Required

> [!definition]
> HTTP 426 is an [HTTP status code](HTTP%20status%20code.md) indicating that the server refuses the request under the current protocol but may accept it after the client upgrades.

RFC 9110 requires a 426 response to include an `Upgrade` header naming acceptable protocols.

```http
HTTP/1.1 426 Upgrade Required
Upgrade: artifact-presigned/1
Content-Type: application/json

{
  "message": "This server requires presigned artifact transfer."
}
```

## Why it is useful

A legacy artifact request is understandable, but the server deliberately no longer accepts that transfer path. A 426 can tell an old client:

- the route is not merely missing;
- retrying the identical request will not help;
- a newer protocol or client behavior is required.

The response body should provide an actionable explanation even when automated clients do not understand the upgrade token.

## Status comparison

| Status | Better fit when... |
|---|---|
| `400 Bad Request` | request syntax or values are invalid |
| `404 Not Found` | resource or route should appear absent |
| `409 Conflict` | request conflicts with current resource state |
| `426 Upgrade Required` | current protocol/path is refused and an upgrade is available |
| `501 Not Implemented` | server does not support the requested functionality |

## Application-level nuance

426 originated for HTTP protocol upgrades. Using it for an application-level artifact-transfer protocol should therefore be deliberate:

- choose and document a meaningful `Upgrade` token;
- include the required header;
- test behavior through proxies;
- ensure clients still receive useful structured error text;
- avoid applying it to unrelated routes.

In [2026-07-26 - Add presigned artifact UI support](../Tasks/2026-07-26%20-%20Add%20presigned%20artifact%20UI%20support.md), only legacy artifact-service upload/download routes return 426. Logged-model and model-version tracking APIs remain available because they are outside that route boundary and lack a replacement in the change.

## Related concepts

- [HTTP status code](HTTP%20status%20code.md)
- [Backward compatibility](Backward%20compatibility.md)
- [Capability negotiation](Capability%20negotiation.md)
- [Fallback behavior](Fallback%20behavior.md)
- [Client-server model](Client-server%20model.md)

## Further reading

- [RFC 9110 §15.5.22: 426 Upgrade Required](https://www.rfc-editor.org/rfc/rfc9110.html#name-426-upgrade-required)
- [RFC 9110 §7.8: Upgrade](https://www.rfc-editor.org/rfc/rfc9110.html#name-upgrade)

