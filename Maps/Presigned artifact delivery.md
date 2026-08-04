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

Use this map to learn the concepts behind [[2026-07-26 - Add presigned artifact UI support]].

## 1. System boundaries

1. [[Client-server model]]
2. [[Environment variable]]
3. [[Configuration ownership]]
4. [[Authentication]]
5. [[Authorization]]

## 2. Selecting a transfer protocol

1. [[Capability]]
2. [[Capability negotiation]]
3. [[Backward compatibility]]
4. [[Fallback behavior]]
5. [[Fail-fast validation]]
6. [[HTTP status code]]
7. [[HTTP 426 Upgrade Required]]

## 3. Moving artifact bytes

1. [[Presigned URLs]]
2. [[Streaming HTTP downloads]]
3. [[Content-Length]]
4. [[Backpressure]]
5. [[Atomic filesystem operation]]

## Guiding question

How can old and new clients choose a compatible artifact-transfer path without allowing compatibility logic to weaken server policy or access control?

