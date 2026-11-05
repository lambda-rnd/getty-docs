# Publication and verification

**Status:** Concept · **Audience:** Streamers, integrators, and researchers

A result visible in getty, an AO message visible in an explorer, and a verified permanent archive describe different stages. This page explains how to interpret them without treating internal state or administrative routes as public API contracts.

## Three questions to ask

| Question                                   | Relevant evidence                                                                                            |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| Was the application action confirmed?      | The authorized primary state and the identified round or session                                             |
| Does AO reflect that state?                | The expected process and scope, matching version, matching payload, and matching digest                      |
| Can a permanent archive be read correctly? | A valid reference, expected owner and content hash, and successful validation of the manifest and its chunks |

An explorer is useful for discovering a transaction or message. Its visibility alone does not establish all three outcomes.

## Verifying a poll or raffle projection

The current production model confirms the interaction in PostgreSQL and publishes a versioned snapshot to AO. A maintainer-controlled comparison can establish that:

1. The intended process and source are being inspected.
2. The published snapshot belongs to the expected module, workspace scope, and round.
3. The primary publication and evaluated AO entry have the same version.
4. The exact serialized payload matches, and its SHA-256 agrees with the recorded digest.
5. The application fields match the expected outcome, such as a closed poll and its option counts.

A digest comparison checks the serialized bytes; reformatting the JSON before hashing can change its digest. Option IDs are identifiers rather than numeric positions. In the [permanent poll result schema](../schemas/poll-result.schema.json), they are strings.

The following is a **synthetic comparison report**, not a supported API response or a production export:

```json
{
  "primaryVersion": 4,
  "aoVersion": 4,
  "publicationStatus": "published",
  "samePayload": true,
  "sameSHA256": true,
  "active": false,
  "totalVotes": 3,
  "options": [
    { "id": "1", "label": "Forest", "votes": 2 },
    { "id": "2", "label": "City", "votes": 1 }
  ]
}
```

Matching bytes and versions demonstrate agreement for that snapshot. They do not establish voter eligibility, upstream data accuracy, complete event history, or the result of a different round. A current projection can advance when another round starts; an intentionally published result record serves a different historical role.

## Projection and permanent result are separate artifacts

An AO snapshot can include a reference to an Arweave result record. Confirming that the snapshot contains the expected reference verifies that association. Independently validating the referenced file requires retrieving and checking that file as well.

The [poll and raffle schemas](../schemas/README.md) describe final records intended for permanent storage. They are not schemas for the full AO process state or for an application publication envelope.

## Stream History verification

The archive workflow publishes a manifest and its sample chunks to Arweave, then registers a lightweight AO reference. Before treating an archive as complete, Getty checks the AO reference and reads the archive with validation of the expected owner, session, manifest hash, chunk hashes, schema, and sample counts.

| State           | User-facing interpretation                                                  |
| --------------- | --------------------------------------------------------------------------- |
| Pending         | Work is queued; publication is not confirmed.                               |
| Processing      | The worker is handling the archive.                                         |
| Verifying       | Publication references exist and verification is still pending.             |
| Complete        | The archive passed the workflow's index and content checks.                 |
| Awaiting wallet | The data owner's storage wallet is missing or unusable for this operation.  |
| Needs attention | Review the feature's explanation before retrying or changing configuration. |

These are explanatory states, not a guarantee of private field names or administrative response formats. Applicable wallet setup remains separate from sign-in; see [Accounts and sign-in](accounts-and-sign-in.md#storage-wallets-are-separate).

An archive with no retained samples must not be presented as a recovered detailed timeline. Preserve the distinction between a summary, observed samples, and unknown intervals. Successful archive verification confirms the archived content, not that collection captured every real-world event.

## Encrypted copies and practical recovery

Selected preference and achievement copies can be encrypted before publication. Their ciphertext and some metadata may be publicly observable and permanent. Decryption depends on the original key material; replacing it does not recover older copies.

AO projections and permanent archives complement the primary store. They do not replace a recovery plan for authoritative databases, required keys, identities, or other application dependencies. Concrete backup schedules and restoration procedures belong in the deployment's private operator documentation.

## Troubleshooting without changing identity

- If a projection is older than the primary state, inspect its publication status and allow the asynchronous workflow to finish.
- If an HTTP response succeeds but the expected data is absent, validate the response representation and requested state key.
- If an archive is verifying, inspect its progress before initiating another upload.
- If a wallet is unavailable, confirm the current workspace and its storage configuration. Another workspace's wallet is not an automatic substitute.
- If samples are missing, preserve available records and investigate a valid historical source. Repeated publication cannot recreate observations that are absent.

Public identifiers are useful references, not proof of ownership or permission to merge accounts. Raw node reads are also distinct from supported Getty APIs; see [Supported public API](public-api.md).

---

[AO, Arweave, and HyperBEAM](ao-arweave-hyperbeam.md) · [Documentation index](index.md) · [Security and privacy](security-and-privacy.md)
