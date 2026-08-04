---
type: map
status: growing
created: 2026-07-30
updated: 2026-07-30
tags:
  - map
  - artifacts
  - distributed-systems
---

# Presigned artifact delivery

Use this map to learn the concepts behind [2026-07-26 - Add presigned artifact UI support](../Tasks/2026-07-26%20-%20Add%20presigned%20artifact%20UI%20support.md).

## 1. System boundaries

1. [Client-server model](../Concepts/Client-server%20model.md)
2. [Environment variable](../Concepts/Environment%20variable.md)
3. [Configuration ownership](../Concepts/Configuration%20ownership.md)
4. [Authentication](../Concepts/Authentication.md)
5. [Authorization](../Concepts/Authorization.md)

## 2. Selecting a transfer protocol

1. [Capability](../Concepts/Capability.md)
2. [Capability negotiation](../Concepts/Capability%20negotiation.md)
3. [Backward compatibility](../Concepts/Backward%20compatibility.md)
4. [Fallback behavior](../Concepts/Fallback%20behavior.md)
5. [Fail-fast validation](../Concepts/Fail-fast%20validation.md)
6. [HTTP status code](../Concepts/HTTP%20status%20code.md)
7. [HTTP 426 Upgrade Required](../Concepts/HTTP%20426%20Upgrade%20Required.md)

## 3. Moving artifact bytes

1. [Presigned URLs](../Concepts/Presigned%20URLs.md)
2. [Streaming HTTP downloads](../Concepts/Streaming%20HTTP%20downloads.md)
3. [Content-Length](../Concepts/Content-Length.md)
4. [Backpressure](../Concepts/Backpressure.md)
5. [Atomic filesystem operation](../Concepts/Atomic%20filesystem%20operation.md)

## Guiding question

How can old and new clients choose a compatible artifact-transfer path without allowing compatibility logic to weaken server policy or access control?

