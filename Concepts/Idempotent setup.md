---
type: concept
status: growing
aliases:
  - idempotent initialization
  - repairable setup
created: 2026-07-30
updated: 2026-07-30
tags:
  - reliability
  - deployment
---

# Idempotent setup

> [!definition]
> Idempotent setup is initialization that can be retried without corrupting the result or producing unintended duplicate effects.

It applies the general property of [Idempotency](Idempotency.md) to installation and resource creation.

## Desired behavior

If `prepare()` succeeds once, calling it again should leave the system in the same valid state:

```text
prepare(prepare(state)) = prepare(state)
```

Real setup often cannot simply repeat every command. Instead it uses a protocol:

```python
with setup_lock:
    if is_complete_and_current():
        return

    if is_incomplete_or_stale():
        remove_or_repair()

    mark_incomplete()
    build()
    validate()
    mark_complete()
```

## Three separate concerns

| Concern | Question | Typical mechanism |
|---|---|---|
| [Mutual exclusion](Mutual%20exclusion.md) | Can two actors run setup together? | [File locking](File%20locking.md) |
| [Crash consistency](Crash%20consistency.md) | Can interrupted work be detected? | marker, journal, transaction |
| Idempotency | Can setup safely run again? | validation, repair, replacement |

A lock alone does not make setup idempotent. It can serialize the same destructive mistake.

## Designing retryable setup

- Define what “complete” means; directory existence is usually too weak.
- Validate a version, manifest, executable, or expected files.
- Treat partial and stale resources as repair cases.
- Avoid irreversible side effects, or record enough information to compensate for them.
- Publish completion only after validation.
- Make cleanup safe when the target is already absent.

## In the MLflow work

In [2026-07-28 - Implement LocalJobExecutor](../Tasks/2026-07-28%20-%20Implement%20LocalJobExecutor.md), a canceled `uv` setup may leave its final directory behind. The next submission takes the lock, notices the incomplete marker, cleans the partial environment, and prepares it again before launching the job.

## Related concepts

- [Idempotency](Idempotency.md)
- [File locking](File%20locking.md)
- [Crash consistency](Crash%20consistency.md)
- [Mutual exclusion](Mutual%20exclusion.md)
- [Durable state](Durable%20state.md)

