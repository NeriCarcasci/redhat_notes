---
type: concept
status: growing
aliases:
  - process ID reuse
created: 2026-07-30
updated: 2026-07-30
tags:
  - operating-systems
  - concurrency
---

# PID reuse

> [!definition]
> PID reuse occurs when the operating system assigns a numeric [Process ID](Process%20ID.md) from a terminated, reaped [Process](Process.md) to a later, unrelated process.

A PID identifies a process only during that process's lifetime. It is not a permanent identity.

## The stale-identity hazard

```mermaid
sequenceDiagram
    participant E as "Executor"
    participant A as "Original process (PID 4100)"
    participant K as "Kernel"
    participant B as "Unrelated process (PID 4100)"

    E->>A: "Check whether PID 4100 is finished"
    A-->>K: "Exit and become reaped"
    K->>B: "Reuse PID 4100"
    E->>B: "Signal stale PID 4100"
```

The dangerous gap is a [TOCTOU race](TOCTOU%20race.md): the executor checks one fact, the system changes, and the executor later acts as if the old fact were still true.

## Risky pattern

```python
if process.poll() is None:
    # Time passes here. The checked identity may no longer be current.
    os.killpg(process.pid, signal.SIGKILL)
```

The exact risk depends on what `poll()` did, which identifiers are reused, and whether the supposed [process group](POSIX%20process%20groups.md) still exists. The broader lesson is not to split identity validation and destructive action across an unprotected interval.

## Mitigation strategies

- Serialize lifecycle decisions with [Mutual exclusion](Mutual%20exclusion.md) so competing executor threads cannot independently complete and cancel the same record.
- Keep the check and signal as one small critical operation.
- Validate structural facts—for example, that a process is still the expected group leader—immediately before signaling.
- Prefer stable kernel handles where the platform supplies them; a raw integer PID is weaker.
- Make signaling helpers report whether they actually delivered a signal, then reconcile with the authoritative process result.

No user-space technique can make an integer PID globally permanent. The goal is to reduce the window and make incorrect state transitions impossible even if signaling loses a race.

## In the MLflow work

[2026-07-28 - Implement LocalJobExecutor](../Tasks/2026-07-28%20-%20Implement%20LocalJobExecutor.md) keeps process-state inspection and group signaling coordinated under the executor's record lock. It avoids a separate `poll()` immediately before signaling and checks that the expected leader still owns the group.

## Related concepts

- [Process ID](Process%20ID.md)
- [Process reaping](Process%20reaping.md)
- [POSIX process groups](POSIX%20process%20groups.md)
- [TOCTOU race](TOCTOU%20race.md)
- [Cancellation races](Cancellation%20races.md)
- [Mutual exclusion](Mutual%20exclusion.md)

## Further reading

- [POSIX process ID and process-group ID definitions](https://pubs.opengroup.org/onlinepubs/9799919799/basedefs/V1_chap03.html)

