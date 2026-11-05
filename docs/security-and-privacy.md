# Security and privacy

**Status:** Stable policy · **Audience:** All readers

Getty Docs publishes information that is useful for understanding and integrating with the application without disclosing private implementation or user data.

## Data classes

| Class                   | Examples                                                   | Documentation rule                                                |
| ----------------------- | ---------------------------------------------------------- | ----------------------------------------------------------------- |
| Public contract         | Widget path, documented schema, public transaction tag     | May be documented                                                 |
| Public but correlatable | Wallet address, process ID, transaction ID                 | Publish only when intentionally designated as a durable reference |
| User configuration      | Widget token, tenant mapping, private stream settings      | Never use production values                                       |
| Secret                  | JWK, signer, session cookie, API credential                | Never publish                                                     |
| Operational             | Host topology, logs, internal routes, defensive thresholds | Keep private unless separately approved                           |

## Immutable data

Data written to Arweave may remain publicly accessible indefinitely. getty modules should publish only the documented payload and should avoid secrets, private account mappings, and unnecessary personal data.

## Selected encrypted copies

The current integration can publish encrypted copies of selected preferences and achievement records. Ciphertext and some metadata remain publicly observable and can be permanent; encryption does not make a transaction private or removable. Protecting the original decryption material remains necessary.

Authentication records, private wallet keys, sign-in mappings, and operational configuration outside the explicit selection are excluded from these copies. Public documentation must still avoid production account mappings, raw snapshots, and operational exports. See [AO copies](ao-arweave-hyperbeam.md#encrypted-achievement-and-preference-copies) and [verification](publication-and-verification.md#encrypted-copies-and-practical-recovery).

## Responsible use

Public documentation is intended for normal integration and research. It does not authorize load testing, access-control bypass attempts, or probing live users and infrastructure.

See [SECURITY.md](../SECURITY.md) for private reporting instructions.

---

[Previous: Supported public API](public-api.md) · [Documentation index](index.md) · [Publication policy](../PUBLICATION_POLICY.md)
