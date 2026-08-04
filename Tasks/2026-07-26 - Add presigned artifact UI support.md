---
type: task
status: active
created: 2026-07-26
updated: 2026-07-30
project: MLflow
tags:
  - work/mlflow
  - artifacts
  - ui
  - python
sources:
  - https://github.com/NeriCarcasci/mlflow/commits/feat/presigned-artifact-ui
  - https://github.com/mlflow/mlflow/pull/24678
---

# Add presigned artifact UI support

## Objective

Allow the MLflow UI and Python artifact client to use backend-generated [Presigned URLs](../Concepts/Presigned%20URLs.md), and add a server mode that requires presigned artifact transfer instead of legacy proxy upload and download routes.

## Context

- Branch: `feat/presigned-artifact-ui`
- Current remote commit: `0c271f9c56a027a50bfcd41e27657e71f8a315c0`
- Earlier UI commit: `f00a73971`
- Local repository: `/Users/ncarcasc/RH_DEV_MAIN/repos/mlflow`
- Upstream PR: not opened at capture time.
- Dependency: centralized `/server-info` behavior from [mlflow/mlflow#24678](https://github.com/mlflow/mlflow/pull/24678).

## Work completed

- Added a UI server-info hook and unified artifact-fetching path.
- Updated artifact, audio, and video views to consume the unified fetch behavior.
- Added server and CLI configuration for presigned-only artifact serving.
- Added Python repository capability detection and presigned upload/download paths.
- Rejected presigned-only startup when the selected artifact backend cannot generate the required signed URLs.
- Parsed `MLFLOW_ARTIFACTS_ONLY_PRESIGNED=false` as false in both Click-driven startup and worker configuration.
- Prevented a server-only environment variable from silently changing Python client policy.
- Required small uploads to perform [Capability negotiation](../Concepts/Capability%20negotiation.md) instead of falling through to legacy upload behavior.
- Streamed downloads directly when server metadata does not include `file_size`.
- Returned actionable [HTTP 426 Upgrade Required](../Concepts/HTTP%20426%20Upgrade%20Required.md) responses from legacy artifact-service upload and download routes in presigned-only mode.
- Kept logged-model and model-version tracking routes available because they are outside the legacy artifact-service proxy boundary and have no equivalent replacement in this change.

## Important decisions

- The server advertises capabilities through `/server-info`; clients derive behavior from that response rather than reading a server configuration variable from their own environment.
- Presigned-only mode fails at startup if the artifact backend cannot fulfill the advertised contract.
- All uploads, including small ones, must honor server capabilities so a presigned-only server is never contacted through a forbidden legacy route.
- A missing `file_size` is not a reason to reject a valid signed download; use [Streaming HTTP downloads](../Concepts/Streaming%20HTTP%20downloads.md) without preallocation.
- Only legacy artifact-service proxy routes return 426. Tracking APIs for logged models and model versions remain available.
- Preserve explicit fallback behavior for servers that do not advertise presigned support, while preventing fallback when the server explicitly requires presigned transfer.

## Review findings resolved

- Invalid backend configuration was accepted until the first transfer attempt.
- The string `"false"` was treated as truthy by direct Python boolean conversion.
- Client behavior could be overridden by a server-scoped environment variable.
- Small uploads bypassed the capability probe.
- Downloads assumed signed responses always contained a size.
- The first route audit was too broad and would have blocked tracking APIs without a replacement.

## Verification

- Ruff passed for affected Python files.
- `git diff --check` passed.
- 127 affected Python tests passed and 10 were skipped.
- 14 focused regression tests covered the review fixes.
- 29 UI tests passed across server-info and unified artifact fetching.
- Live cloud integration behavior for S3, GCS, and Azure—including credentials, prefixes, and workspaces—remains an explicit residual risk.

## Outcome

The two local commits are pushed to `origin/feat/presigned-artifact-ui`. The task remains active because no upstream MLflow PR exists yet and the branch should be reconciled with the merged/final form of PR #24678 before submission.

## Concepts encountered

- [Presigned URLs](../Concepts/Presigned%20URLs.md)
- [Capability negotiation](../Concepts/Capability%20negotiation.md)
- [Configuration ownership](../Concepts/Configuration%20ownership.md)
- [Fail-fast validation](../Concepts/Fail-fast%20validation.md)
- [HTTP 426 Upgrade Required](../Concepts/HTTP%20426%20Upgrade%20Required.md)
- [Streaming HTTP downloads](../Concepts/Streaming%20HTTP%20downloads.md)
- [Fallback behavior](../Concepts/Fallback%20behavior.md)

## Follow-up

- Rebase or restack the branch on the final centralized `/server-info` implementation.
- Confirm the final server-info response property used to advertise presigned-only behavior.
- Run live object-store integration tests where credentials are available.
- Squash and open the upstream PR with the dependency/order made explicit.

