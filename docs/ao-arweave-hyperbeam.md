# AO, Arweave, and HyperBEAM

**Status:** Concept · **Audience:** Developers and researchers

getty combines hosted coordination with permanent storage and decentralized compute. Arweave, AO, and HyperBEAM are related, but they are not interchangeable and do not hold the same data.

| Component | getty use |
| --- | --- |
| Arweave | Permanent assets, selected result records, and stream archives |
| AO | Optional decentralized state, computation, and lightweight archive indexes |
| HyperBEAM | HTTP-readable access to materialized AO process state |

> [!IMPORTANT]
> An AO process is network-resident. It is not a daemon running inside the getty application server, and an interactive AOS session does not need to remain open for the process to continue existing.

## How the pieces fit together

For an AO-backed interaction, getty's hosted layer authenticates and authorizes the action before submitting a signed message to an AO process. HyperBEAM materializes selected process state into HTTP-readable views. getty can then normalize that state for its public APIs, administration UI, and overlays.

```text
Streamer action
      |
      v
getty hosted authorization -- signed message --> AO process
      ^                                             |
      |                                             v
      +----------- normalized read ---------- HyperBEAM
```

The hosted layer remains responsible for authentication, write authorization, public response contracts, WebSocket delivery, and compatibility behavior. AO does not expose private signing material to an overlay or browser.

## Module responsibilities

Deployments can enable AO independently for supported modules.

| Module | Decentralized responsibility |
| --- | --- |
| Polls | Poll lifecycle, options, votes, countdown state, and result state when the AO backend is enabled |
| Raffle | Raffle state, participants, draw state, and winner history when the AO backend is enabled |
| Achievements | Achievement definitions and progress state when the AO backend is enabled |
| Stream History | A lightweight index that links a stream to its verified Arweave archive |

The presence of an AO process does not imply that every module or every deployment uses AO as its active backend. getty can retain hosted coordination where it is required for authentication, delivery, or compatibility.

## Arweave records

When permanent results are enabled and a compatible wallet is configured, getty can publish selected poll or raffle result payloads. See the schemas in [`schemas/`](../schemas/README.md).

Publishing is an explicit module-level action. A result shown by getty is not necessarily permanent unless it includes a confirmed Arweave transaction reference.

The public poll and raffle schemas describe final result records intended for permanent publication. They do not describe transient module state or the complete state of an AO process.

Arweave can also hold immutable widget entry documents and verified Stream History archives. A Permaweb widget can load its entry document from Arweave while continuing to use supported getty services for live state and delivery.

> [!WARNING]
> Arweave data is designed to be permanent. Payloads must exclude secrets, private account mappings, unnecessary personal data, and any field that is not intended for durable public access.

## Stream History archives

Stream History separates live operational data from permanent archives:

1. getty keeps live and pending stream data in its operational store.
2. After a stream closes, eligible archive content is packaged and published to Arweave.
3. The archive manifest identifies its schema, content, and referenced chunks.
4. A lightweight reference is registered in the AO Stream History process.
5. getty verifies both the AO reference and the Arweave content before treating the archive as complete.

AO stores the index and archive pointer, not a second copy of every stream sample. Arweave is the permanent content source for a completed archive.

### Stream History upload cost

Stream History is free by design. Getty compresses and divides analytics into objects that remain eligible for Turbo's free upload route. Each permanent Stream History object stays within the 100 KiB free limit; sample chunks target 90 KB to leave room for the archive envelope metadata.

The final archive manifest is also bounded for the free route. If an archive cannot satisfy those bounds, getty reports the archive as needing attention. It does not silently switch Stream History to a paid Arweave transaction, consume Turbo credits, or spend native AR.

The wallet configured for the data owner signs the archive. A namespaced Stream History upload does not fall back to a server wallet when the tenant wallet is missing or temporarily unavailable.

### Native AR policy for permanent media

The native AR spending policy applies to an individual permanent media file that exceeds Turbo's 100 KiB free limit. It does not apply to Stream History analytics. Arweave-backed media can include notification images or video, Tip Goal and achievement audio, raffle and announcement images, Liveviews icons, and external-live media.

The account owner selects one of three modes:

| Mode | Behavior for a media file over 100 KiB |
| --- | --- |
| Free only | The upload is rejected without spending AR. |
| Ask for approval | Getty shows the estimated AR cost and uploads only after approval for that request. Cancelling leaves no paid-upload backlog. |
| Protected automatic | Getty may pay automatically only within the configured per-upload maximum and protected wallet reserve. |

Files at or below 100 KiB continue through Turbo's free route in every mode. A direct paid upload is limited to 12 MiB per file.

Automatic payment requires explicit recorded consent. Replacing the wallet resets the policy to **Free only**, and wallet-bound payment authorization is not restored through a configuration import. The account's wallet signs and pays an authorized direct upload; the server wallet is not a payment fallback.

> [!IMPORTANT]
> Approval is scoped to the current media upload. A rejected, cancelled, over-limit, or unfunded request must not become an authorized payment later.

## AO state

An AO process has a durable identifier and receives signed messages. Its state can evolve as those messages are evaluated. Process ownership, runtime signing, and end-user storage authorization are distinct roles:

- A process owner can perform process-level administration.
- A getty runtime signer can submit only the application actions it is authorized to perform.
- A tenant wallet signs permanent publication and can authorize applicable media storage spending for that tenant's data. Stream History archives remain on the free route.

> [!IMPORTANT]
> Public wallet addresses and process identifiers are not secrets, but they are correlatable. Private JWK material, signer configuration, owner mappings, and authorization rules must remain outside public documentation and client-side code.

AO process identifiers are public blockchain identifiers, but Getty documents only identifiers that maintainers intentionally declare as supported public references. Examples use placeholders:

```text
<ao-process-id>
```

## HyperBEAM reads

HyperBEAM can expose AO state through HTTP routes. A missing state key does not, by itself, prove that an AO process is unavailable; it can mean that the requested key has not been materialized.

Process availability and state-key availability are separate checks:

- The process endpoint indicates whether the process can be resolved.
- A compute path addresses one materialized portion of its state.
- getty's public API can adapt that state into a stable, module-specific response.

Consumers should use supported getty APIs when they need a stable integration contract. Raw HyperBEAM state reflects the AO process representation and can change independently of the public API.

## Public verification boundary

Arweave transaction IDs, intentionally published AO process IDs, payload schemas, and content hashes can support independent verification. A public identifier proves neither authorization nor ownership of an unrelated getty account.

Exact production nodes, internal fallback behavior, write signers, and unpublished process mappings are outside this repository's scope.

---

[Previous: Overlays and OBS](overlays.md) · [Documentation index](index.md) · [Next: Analytics](analytics/index.md)
