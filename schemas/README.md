# Public schemas

**Status:** Preview · **Audience:** Integrators and developers

Machine-readable schemas describe getty payloads that can be published to permanent storage.

- [Poll result schema](poll-result.schema.json)
- [Raffle result schema](raffle-result.schema.json)

Schemas document payload shape, not proof that a particular record was successfully uploaded or finalized.

These schemas describe final result records intended for permanent publication. They do not describe transient poll or raffle state, or the complete state of their AO processes.

Each schema uses a versioned `urn:getty:schema:...` identifier so its canonical identity does not depend on a documentation host. Consumers should select a schema by the payload's `schema` value and must not assume that a schema identifier is a downloadable URL.

---

[Documentation index](../docs/index.md) · [Synthetic examples](../examples/README.md) · [AO, Arweave, and HyperBEAM](../docs/ao-arweave-hyperbeam.md)
