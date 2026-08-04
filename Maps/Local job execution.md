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

Use this map to learn the concepts behind [[2026-07-28 - Implement LocalJobExecutor]].

## 1. Process foundations

Start with:

1. [[Process]]
2. [[Process ID]]
3. [[Child process]]
4. [[POSIX session]]
5. [[POSIX process groups]]
6. [[Unix signal]]
7. [[Process reaping]]

## 2. Concurrent lifecycle decisions

Then study:

1. [[Race condition]]
2. [[Mutual exclusion]]
3. [[Linearization point]]
4. [[Cancellation races]]
5. [[TOCTOU race]]
6. [[PID reuse]]

## 3. Recoverable environment setup

Finally:

1. [[File locking]]
2. [[Durable state]]
3. [[Atomic filesystem operation]]
4. [[Crash consistency]]
5. [[Idempotency]]
6. [[Idempotent setup]]

## Guiding question

How can an executor ensure that every submitted job reaches one truthful terminal result while leaving neither descendant processes nor partially valid environments behind?

