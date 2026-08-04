---
type: concept
status: growing
aliases:
  - fail-fast configuration
  - startup validation
created: 2026-07-30
updated: 2026-07-30
tags:
  - reliability
  - configuration
---

# Fail-fast validation

> [!definition]
> Fail-fast validation rejects an invalid configuration at the earliest reliable boundary, before the system begins normal work.

## Why early failure is valuable

Suppose a server advertises presigned-only transfer but its artifact backend cannot create [Presigned URLs](Presigned%20URLs.md). Without startup validation:

1. deployment appears healthy;
2. users can create runs;
3. the first artifact transfer fails later;
4. the failure appears far from the configuration mistake.

Failing startup makes the invalid combination visible to the deployer and prevents a partially usable service from accepting traffic.

```python
def validate_server_config(config, artifact_repository):
    if config.presigned_only and not artifact_repository.supports_presigned_urls:
        raise ConfigurationError(
            "Presigned-only mode requires an artifact backend "
            "that supports presigned upload and download."
        )
```

## What to validate early

- mutually incompatible options;
- required credentials or dependencies that can be checked safely;
- selected implementation satisfies a required [Capability](Capability.md);
- values have valid syntax and range;
- a security policy can actually be enforced.

## What may remain runtime-only

- temporary network reachability;
- per-user [Authorization](Authorization.md);
- object-specific permissions;
- resources created after startup;
- transient provider failures.

Fail-fast does not mean “perform every possible operation during startup.” It means reject states already known to be invalid.

## Operational qualities of a good error

- names the conflicting settings;
- identifies the incapable component;
- explains an actionable fix;
- avoids leaking secrets;
- occurs before readiness is reported.

## In the MLflow work

[2026-07-26 - Add presigned artifact UI support](../Tasks/2026-07-26%20-%20Add%20presigned%20artifact%20UI%20support.md) validates the artifact backend when presigned-only mode is enabled. This aligns advertised [capabilities](Capability%20negotiation.md) with executable behavior.

## Related concepts

- [Capability](Capability.md)
- [Configuration ownership](Configuration%20ownership.md)
- [Environment variable](Environment%20variable.md)
- [Presigned URLs](Presigned%20URLs.md)
- [Fallback behavior](Fallback%20behavior.md)

