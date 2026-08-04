---
type: concept
status: growing
aliases:
  - flow control
created: 2026-07-30
updated: 2026-07-30
tags:
  - performance
  - distributed-systems
---

# Backpressure

> [!definition]
> Backpressure is a flow-control effect in which a slower consumer limits how quickly a producer sends or queues more work.

Without backpressure, a fast network reader and slow disk writer can accumulate unbounded data in memory. In [[Streaming HTTP downloads]], sequentially awaiting reads and writes keeps only a bounded amount of data in flight.

Backpressure may be implemented through bounded queues, demand signals, paused reads, window sizes, or blocking writes.

## Related concepts

- [[Streaming HTTP downloads]]
- [[Content-Length]]
- [[Client-server model]]

