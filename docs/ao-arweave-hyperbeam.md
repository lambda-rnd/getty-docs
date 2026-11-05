# AO, Arweave, and HyperBEAM

**Status:** Concept · **Audience:** Developers and researchers

Getty uses PostgreSQL-confirmed application state, AO projections, and permanent Arweave records for different purposes. The current production integration operates through a getty-managed HyperBEAM node. This page describes the roles of those components without making deployment endpoints or raw process representations a supported public API.

| Component  | Role in the current integration                                                          |
| ---------- | ---------------------------------------------------------------------------------------- |
| PostgreSQL | Primary application state for the integrated modules                                     |
| AO         | Versioned public projections, selected encrypted copies, and lightweight archive indexes |
| HyperBEAM  | AO process execution and HTTP-readable state inspection                                  |
| Arweave    | Permanent assets, selected final results, and stream archive content                     |

## How the pieces fit together

For polls and raffles, getty authorizes an interaction and confirms the primary change in PostgreSQL. An asynchronous worker then submits a signed, versioned snapshot to AO. HyperBEAM evaluates the message and exposes the resulting state for inspection. Getty's hosted services continue to provide supported APIs, WebSocket delivery, and overlay updates.

```text
Authorized action -> PostgreSQL commit -> Versioned snapshot -> AO projection
                             |                                  |
                             |                           HyperBEAM inspection
                             v
                 Eligible permanent record -> Arweave
```

The projection represents committed state. Retrying its publication does not cast another vote or draw another winner. Publication can lag behind the primary change, and intermediate changes can coalesce into a later snapshot. A projection is not a complete event log.

AO processes have durable identifiers and message-based state. A process identity is separate from the Getty HTTP service and from the HyperBEAM runtime that evaluates it; an interactive AOS terminal does not need to remain open.

## Module responsibilities

| Module           | Current AO responsibility                                         | Primary behavior                                                                        |
| ---------------- | ----------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Polls            | Public projection of lifecycle, options, counts, and result state | PostgreSQL confirms the interaction.                                                    |
| Raffle           | Public projection of confirmed raffle state and results           | PostgreSQL confirms the operation. A projection retry does not repeat the draw.         |
| Achievements     | Encrypted copy of selected configuration and progress             | PostgreSQL remains primary for hosted progress and delivery.                            |
| User preferences | Encrypted copy of an explicit set of eligible preferences         | Authentication and operational settings remain outside the copy's scope.                |
| Stream History   | Lightweight references to verified permanent archives             | Operational data and archive jobs are maintained separately from the permanent content. |

Modules may share a projection process. The existence of a process is not evidence that the process is the authoritative backend for every module or workspace. Deployment-specific legacy modes must be evaluated separately.

## Encrypted achievement and preference copies

Selected records are encrypted before publication using authenticated encryption. The current integration uses AES-256-GCM and pseudonymous workspace identifiers. Each copy is associated with its source, module, scope, and version.

Configuration and achievement progress that already existed can be included in the initial copy; later synchronization includes subsequent committed changes. This is a selected state snapshot, not a full backup of the account or every event between synchronizations.

The publication scope excludes credentials, private wallet keys, authentication/session records, private sign-in mappings, and other operational data outside the explicit selection. Ciphertext and metadata can still remain publicly observable. Retaining the original decryption material is necessary to recover an older encrypted copy.

## Arweave records

Where permanent results are enabled and the authorized storage requirements are met, getty can publish selected poll or raffle result payloads. See the [public schemas](../schemas/README.md).

A result shown by getty, a successful AO projection, and a permanent result record are separate facts. A projection can include an Arweave reference, but validating the referenced file is an additional step. See [Publication and verification](publication-and-verification.md).

The poll and raffle schemas describe final result records intended for permanent publication. They do not describe transient module state or the complete AO process representation.

Arweave can also hold immutable widget entry documents and verified Stream History archives. A Permaweb widget can load its entry document from Arweave while continuing to use getty for live state and delivery.

> [!WARNING]
> Permanently published plaintext must be intentionally public. Exclude secrets, private account mappings, and unnecessary personal data. Encrypted copies also need deliberate selection and key protection because their ciphertext remains durable.

## Stream History archives

Stream History separates operational observations from permanent archives:

1. getty retains the available stream observations and archive job state.
2. Eligible closed sessions are packaged into a manifest and sample chunks.
3. The configured data owner's wallet signs publication to Arweave.
4. getty registers a lightweight archive reference in AO.
5. The workflow checks the AO reference and validates the manifest and chunks before marking the archive complete.

AO holds the archive index, not another full copy of every stream sample. Existing permanent archives retain their original verified publication owner independently of a later sign-in or wallet change.

Missing wallet configuration leaves work pending; it does not authorize a server-wallet substitute. A session with a summary but no recoverable samples must remain distinguishable from a complete detailed timeline. Permanent archival also does not remove the need for primary data retention and recovery procedures.

Where observed-source history is enabled, an archive can retain channel observations and collection-quality information. Earlier archives without those fields do not acquire them retroactively. Selected channel identifiers and metrics can become permanently public with the archive; private sign-in mappings and credentials are excluded. This page does not define a new archive schema.

### Stream History upload cost

Stream History is free by design. Getty compresses and divides analytics into objects that remain eligible for Turbo's free upload route. Each permanent Stream History object stays within the 100 KiB free limit; sample chunks target 90 KB to leave room for the archive envelope metadata.

The final archive manifest is also bounded for the free route. If an archive cannot satisfy those bounds, getty reports the archive as needing attention. It does not silently switch Stream History to a paid Arweave transaction, consume Turbo credits, or spend native AR.

The wallet configured for the data owner signs the archive. A namespaced Stream History upload does not fall back to a server wallet when the tenant wallet is missing or temporarily unavailable.

### Native AR policy for permanent media

The native AR spending policy applies to an individual permanent media file that exceeds Turbo's 100 KiB free limit. It does not apply to Stream History analytics. Arweave-backed media can include notification images or video, Tip Goal and achievement audio, raffle and announcement images, Liveviews icons, and external-live media.

The account owner selects one of three modes:

| Mode                | Behavior for a media file over 100 KiB                                                                                        |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Free only           | The upload is rejected without spending AR.                                                                                   |
| Ask for approval    | Getty shows the estimated AR cost and uploads only after approval for that request. Cancelling leaves no paid-upload backlog. |
| Protected automatic | Getty may pay automatically only within the configured per-upload maximum and protected wallet reserve.                       |

Files at or below 100 KiB continue through Turbo's free route in every mode. A direct paid upload is limited to 12 MiB per file.

Automatic payment requires explicit recorded consent. Replacing the wallet resets the policy to **Free only**, and wallet-bound payment authorization is not restored through a configuration import. The account's wallet signs and pays an authorized direct upload; the server wallet is not a payment fallback.

> [!IMPORTANT]
> Approval is scoped to the current media upload. A rejected, cancelled, over-limit, or unfunded request must not become an authorized payment later.

## Process ownership and storage authorization

AO messages are signed, but several roles remain distinct:

- A process owner can perform the process-level administration it is authorized to perform.
- The application signer submits the application messages permitted by the process.
- A workspace storage wallet signs its eligible permanent uploads and authorizes applicable media spending. Stream History archives remain on the free route.

A public process ID, transaction ID, or wallet address is not proof of ownership of another getty workspace. Public identifiers can also be correlated, so examples use placeholders and synthetic values:

```text
<ao-process-id>
```

## HyperBEAM reads

HyperBEAM evaluates messages and exposes selected AO process state through HTTP. The integration has been validated with HyperBEAM v0.11. A route pattern for a process state read is:

```text
https://hyperbeam.example.invalid/<ao-process-id>~process@1.0/compute/<state-key>
```

This is a synthetic, version-dependent HyperBEAM illustration, not a getty API endpoint. Compute can evaluate scheduled messages; the response may contain a JSON wrapper, linked state, or commitments rather than the final application object. A successful HTTP status alone is not a complete state check.

A missing state key can produce `not_found` even when the node and process are otherwise available. Check the intended process, requested field, response representation, and version before concluding that the whole node is down.

Consumers needing a supported integration should use [Getty's public API](public-api.md). Raw HyperBEAM state can evolve independently of that contract. Node administration, deployment addresses, signing configuration, and internal publication interfaces are outside this public repository.

## Earlier descriptions and compatibility

Earlier material described configurations in which AO was the primary interactive backend. That is not the PostgreSQL-primary, projection-based production model described here. A legacy process can also expect different handlers and state keys; changing only its identifier does not migrate its contract.

Moving to a new projection or archive index does not automatically move a process's scheduler, replay its entire execution history, recover missing observations, or transfer old publication ownership. Permanent references, current primary state, process identity, and storage authorization must be reviewed separately.

## Public verification boundary

Public schemas, intentionally published records, and content hashes help readers inspect results. [Publication and verification](publication-and-verification.md) explains the difference between an application result, an evaluated AO projection, an Arweave reference, and a fully checked stream archive.

Exact production nodes, private account identifiers, operational logs, recovery scripts, and unpublished process mappings remain outside the public documentation. This page adds no new supported administrative or write API.

## Further reading

- [AO](https://ao.arweave.net/)
- [Arweave](https://www.arweave.org/)
- [HyperBEAM documentation](https://hyperbeam.arweave.net/)
- [HyperBEAM v0.11 release](https://github.com/permaweb/HyperBEAM/releases/tag/v0.11)

---

[Previous: Overlays and OBS](overlays.md) · [Documentation index](index.md) · [Next: Publication and verification](publication-and-verification.md)
