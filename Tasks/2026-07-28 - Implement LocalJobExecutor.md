---
type: task
status: active
created: 2026-07-28
updated: 2026-07-30
project: MLflow
tags:
  - work/mlflow
  - jobs
  - python
sources:
  - https://github.com/mlflow/mlflow/pull/24680
  - https://issues.redhat.com/browse/RHOAIENG-56601
---

# Implement LocalJobExecutor

## Objective

Implement the in-process `LocalJobExecutor` described by RFC 0002 for RHOAIENG-56601, including submission, terminal results, cancellation, timeouts, restart recovery, and safe environment preparation.

## Context

- Epic: RHOAIENG-56594
- Ticket: RHOAIENG-56601
- Branch: `local-job-executor`
- Base branch: `jobs-execution-rfc2`
- Upstream PR: [mlflow/mlflow#24680](https://github.com/mlflow/mlflow/pull/24680)
- Current commit: `b134150661fd0af4796e0c87941bd4dccc8d491c`
- Local worktree: `/Users/ncarcasc/RH_DEV_MAIN/repos/mlflow-rhoaieng-56601`

## Work completed

- Added the local executor in `mlflow/server/jobs/local_executor.py`.
- Extracted shared subprocess preparation in `mlflow/server/jobs/utils.py` without changing the established Huey execution path.
- Added guarded environment setup in `mlflow/server/jobs/_job_env_setup.py`.
- Implemented job submission, result collection, cancellation, configured timeouts, shutdown behavior, and restart-time requeue behavior.
- Made both setup and job subprocesses members of dedicated POSIX process groups so termination also reaches inherited descendants.
- Reaped direct child processes after signaling them.
- Added repair behavior for interrupted environment creation using a setup lock and incomplete marker.
- Added focused unit and real-subprocess coverage across three test modules.
- Addressed four upstream review threads and replied with the implemented changes.

## Important decisions

- Signal a job's entire [process group](../Concepts/POSIX%20process%20groups.md), not only its direct child process, because job code can create descendants.
- Keep signaling and job-state inspection coordinated under the executor record lock to reduce [PID reuse](../Concepts/PID%20reuse.md) hazards.
- Treat cancellation as a state transition that may lose a [cancellation race](../Concepts/Cancellation%20races.md) to natural completion; if it loses, return the authoritative completed result.
- Keep environment preparation as visible, cancellable executor work instead of hiding it inside the final job command.
- Build virtual environments at their final path because their files can contain absolute paths and are not reliably relocatable.
- Use [File locking](../Concepts/File%20locking.md) plus a persistent incomplete marker to make shared setup repairable after cancellation or a crash.
- Preserve Huey compatibility by sharing command preparation while allowing Huey to execute setup synchronously.
- Keep timeout results distinct from user cancellation and include the job ID, function, and configured timeout in the error.
- Point validation failures to the public `mlflow.server.jobs.job` decorator.

## Review-driven risks covered

- Descendant processes surviving cancellation, timeout, shutdown, or recovery.
- Direct children becoming [zombie processes](../Concepts/Process%20reaping.md) when their exit status is not collected.
- A recycled PID accidentally identifying an unrelated process group.
- Cancellation racing with process completion.
- Cancellation during `uv` environment creation leaving a directory that appears valid but is incomplete.
- Multiple jobs concurrently preparing the same environment.

## Verification

- The final signed commit changes six files: three implementation modules and three test modules.
- The test suite includes real-process descendant cleanup, completion/cancellation races, canceled setup repair, and timeout-result coverage.
- The PR's DCO check passed.
- At capture time, the PR is open. Several upstream checks are failing and require separate triage before merge; this note does not classify those failures as caused by this change.

## Outcome

The implementation and review fixes are pushed as one signed commit. The task remains active until PR #24680 is accepted and merged.

## Concepts encountered

- [POSIX process groups](../Concepts/POSIX%20process%20groups.md)
- [Process reaping](../Concepts/Process%20reaping.md)
- [PID reuse](../Concepts/PID%20reuse.md)
- [Cancellation races](../Concepts/Cancellation%20races.md)
- [File locking](../Concepts/File%20locking.md)
- [Crash consistency](../Concepts/Crash%20consistency.md)
- [Idempotent setup](../Concepts/Idempotent%20setup.md)

## Follow-up

- Triage the remaining PR checks and distinguish branch failures from unrelated upstream failures.
- Follow up on reviewer responses and resolve threads when accepted.
- Record the final merge outcome and any post-review changes here.

