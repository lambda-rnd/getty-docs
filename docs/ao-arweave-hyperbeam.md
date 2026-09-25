# AO, Arweave, and HyperBEAM

**Status:** Concept · **Audience:** Developers and researchers

These systems have separate responsibilities on getty.

| Component | getty use                                             |
| --------- | ----------------------------------------------------- |
| Arweave   | Permanent assets and selected result records          |
| AO        | Optional decentralized state and computation          |
| HyperBEAM | HTTP-readable access to materialized AO process state |

## Arweave records

When permanent results are enabled and a compatible wallet is configured, getty can publish selected poll or raffle result payloads. See the schemas in [`schemas/`](../schemas/README.md).

Publishing is an explicit module-level action. A result shown by getty is not necessarily permanent unless it includes a confirmed Arweave transaction reference.

The public poll and raffle schemas describe final result records intended for permanent publication. They do not describe transient module state or the complete state of an AO process.

## AO state

AO process identifiers are public blockchain identifiers, but getty documents only identifiers that maintainers intentionally declare as supported public references. Examples use placeholders:

```text
<ao-process-id>
```

## HyperBEAM reads

HyperBEAM can expose AO state through HTTP routes. A missing state key does not, by itself, prove that an AO process is unavailable; it can mean that the requested key has not been materialized.

Exact production nodes, internal fallback behavior, write signers, and unpublished process mappings are outside this repository's scope.

---

[Previous: Overlays and OBS](overlays.md) · [Documentation index](index.md) · [Next: Analytics](analytics/index.md)
