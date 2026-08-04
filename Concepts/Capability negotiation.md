---
type: concept
status: growing
aliases:
  - feature negotiation
  - server capability discovery
created: 2026-07-30
updated: 2026-07-30
tags:
  - distributed-systems
  - api-design
---

# Capability negotiation

> [!definition]
> Capability negotiation is a protocol in which participants discover supported behavior and choose a mutually compatible path.

A [[Capability]] describes what a component can do. Negotiation turns that description into a runtime decision, which is especially useful during rolling upgrades and mixed client/server versions.

## The three-state problem

For compatibility, a client often needs more than a Boolean:

| Discovery result | Meaning | Possible client behavior |
|---|---|---|
| Property is `true` | Server explicitly supports or requires feature | Use the new path |
| Property is `false` | Server explicitly does not support feature | Use allowed old path or fail |
| Endpoint/property absent | Older server; capability is unknown | Apply documented legacy behavior |

Conflating “absent” with “false” can break [[Backward compatibility]]. Conflating “false” with a transient discovery error can produce unsafe [[Fallback behavior]].

## MLflow example

```mermaid
flowchart TD
    A["Client requests /server-info"]
    A --> B{"Endpoint available?"}
    B -- "No: older server" --> C["Documented legacy behavior"]
    B -- "Yes" --> D{"Presigned capability"}
    D -- "Supported" --> E["Request presigned transfer"]
    D -- "Required" --> F["Never use legacy proxy"]
    D -- "Unsupported" --> G["Use permitted fallback or fail"]
```

The response belongs to the server-client protocol. A client should not infer the server's state from a local [[Environment variable]]; that would violate [[Configuration ownership]].

## Caching

Capability responses are attractive to cache because they change rarely, but cache scope matters:

- key by complete server identity, including base URL or workspace prefix;
- share successful results where useful;
- avoid permanently caching transient 500 or network failures;
- bound memory use;
- deduplicate identical requests already in flight;
- define behavior when the server changes during the cache lifetime.

This connects the UI work to the centralized `/server-info` work in PR #24678.

## Design questions

- Is the property descriptive (“supports X”) or prescriptive (“requires X”)?
- Does a missing endpoint identify an old server or a broken deployment?
- Which errors allow fallback?
- Is the capability stable enough for process-wide caching?
- Does every code path—including small uploads—consult the same decision?

## In the MLflow work

[[2026-07-26 - Add presigned artifact UI support]] requires capability discovery for all artifact sizes. A server that requires presigned transfer cannot allow the client to skip discovery and use a legacy route for small files.

## Related concepts

- [[Capability]]
- [[Backward compatibility]]
- [[Fallback behavior]]
- [[Client-server model]]
- [[Configuration ownership]]
- [[Fail-fast validation]]

