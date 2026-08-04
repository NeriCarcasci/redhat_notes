---
type: map
status: growing
created: 2026-07-30
updated: 2026-07-30
tags:
  - map
  - jobs
  - operating-systems
---

# Local job execution

Use this map to learn the concepts behind [2026-07-28 - Implement LocalJobExecutor](../Tasks/2026-07-28%20-%20Implement%20LocalJobExecutor.md).

## 1. Process foundations

Start with:

1. [Process](../Concepts/Process.md)
2. [Process ID](../Concepts/Process%20ID.md)
3. [Child process](../Concepts/Child%20process.md)
4. [POSIX session](../Concepts/POSIX%20session.md)
5. [POSIX process groups](../Concepts/POSIX%20process%20groups.md)
6. [Unix signal](../Concepts/Unix%20signal.md)
7. [Process reaping](../Concepts/Process%20reaping.md)

## 2. Concurrent lifecycle decisions

Then study:

1. [Race condition](../Concepts/Race%20condition.md)
2. [Mutual exclusion](../Concepts/Mutual%20exclusion.md)
3. [Linearization point](../Concepts/Linearization%20point.md)
4. [Cancellation races](../Concepts/Cancellation%20races.md)
5. [TOCTOU race](../Concepts/TOCTOU%20race.md)
6. [PID reuse](../Concepts/PID%20reuse.md)

## 3. Recoverable environment setup

Finally:

1. [File locking](../Concepts/File%20locking.md)
2. [Durable state](../Concepts/Durable%20state.md)
3. [Atomic filesystem operation](../Concepts/Atomic%20filesystem%20operation.md)
4. [Crash consistency](../Concepts/Crash%20consistency.md)
5. [Idempotency](../Concepts/Idempotency.md)
6. [Idempotent setup](../Concepts/Idempotent%20setup.md)

## Guiding question

How can an executor ensure that every submitted job reaches one truthful terminal result while leaving neither descendant processes nor partially valid environments behind?

