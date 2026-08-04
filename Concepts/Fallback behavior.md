---
type: concept
status: growing
aliases:
  - compatibility fallback
  - graceful fallback
created: 2026-07-30
updated: 2026-07-30
tags:
  - api-design
  - compatibility
---

# Fallback behavior

> [!definition]
> Fallback behavior selects an older, simpler, or alternate path when the preferred path is unavailable.

Fallback supports [Backward compatibility](Backward%20compatibility.md), but it can also hide defects or violate policy. A safe design defines exactly which evidence permits it.

## Decision table

| Situation | Safe default |
|---|---|
| Old server has no discovery endpoint | Use documented legacy behavior |
| Server explicitly supports presigned transfer | Use [Presigned URLs](Presigned%20URLs.md) |
| Server explicitly requires presigned transfer | Never use legacy proxy |
| Server explicitly says capability unsupported | Use legacy only if policy permits |
| Discovery returns transient 500 or network error | Surface or retry; do not silently reinterpret policy |
| New transfer fails after partially writing data | Clean up and follow operation-specific retry rules |

## Why “unknown” differs from “no”

```mermaid
flowchart TD
    A["Capability result"]
    A --> B["Supported"]
    A --> C["Unsupported"]
    A --> D["Unknown / old server"]
    A --> E["Discovery failed"]

    B --> F["Preferred path"]
    C --> G["Documented allowed alternative"]
    D --> H["Legacy compatibility rule"]
    E --> I["Retry or error"]
```

Treating all non-success cases as “use legacy” creates a fail-open system. A server might be temporarily unable to advertise that legacy transfer is forbidden.

## Questions for every fallback

- Which exact error or response triggers it?
- Is the alternate path semantically equivalent?
- Could it weaken [Authorization](Authorization.md) or another security guarantee?
- Is the operation safe to retry?
- Will telemetry reveal that fallback occurred?
- When can the fallback be removed?

## Avoid fallback loops

The client should not bounce indefinitely between new and legacy paths. Record the chosen policy for one operation, cap retries, and return the most actionable error.

## In the MLflow work

[2026-07-26 - Add presigned artifact UI support](../Tasks/2026-07-26%20-%20Add%20presigned%20artifact%20UI%20support.md) preserves legacy behavior for old servers but prevents fallback when `/server-info` says presigned transfer is required. Even small uploads must perform [Capability negotiation](Capability%20negotiation.md).

## Related concepts

- [Backward compatibility](Backward%20compatibility.md)
- [Capability negotiation](Capability%20negotiation.md)
- [Fail-fast validation](Fail-fast%20validation.md)
- [Authorization](Authorization.md)
- [HTTP 426 Upgrade Required](HTTP%20426%20Upgrade%20Required.md)

