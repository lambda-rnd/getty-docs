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

## Responsible use

Public documentation is intended for normal integration and research. It does not authorize load testing, access-control bypass attempts, or probing live users and infrastructure.

See [SECURITY.md](../SECURITY.md) for private reporting instructions.

---

[Previous: Supported public API](public-api.md) · [Documentation index](index.md) · [Publication policy](../PUBLICATION_POLICY.md)
