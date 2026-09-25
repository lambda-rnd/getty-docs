# Public Documentation Policy

Getty Docs is a curated public knowledge base, not a mirror of getty's private implementation.

## Publication boundary

Content may be published when it is intentionally public, useful to users or integrators, and safe to aggregate. Technical accessibility alone does not make information appropriate for documentation.

### Allowed

- Conceptual architecture and data flow.
- Stable public widget URLs and supported read-only API contracts.
- Public payload schemas and transaction tags.
- Synthetic examples and troubleshooting guidance.
- Publicly announced AO processes or Arweave transactions when they are intended to be durable public references.

### Prohibited

- Credentials, signing material, secrets, or authentication and session data.
- Private identifiers, account mappings, or user data that is not intentionally public.
- Non-public implementation, infrastructure, operational, or security details.
- Raw exports or automatic mirrors from private sources.

## Examples

All examples must use clearly synthetic values. Public tokens and read-only identifiers can still enable correlation or scraping and must never be copied from production.

## Review workflow

1. Author or update content specifically for this repository.
2. Check every identifier, URL, screenshot, and code block.
3. Run secret scanning and link/schema validation.
4. Require maintainer review for API, schema, process-ID, and security changes.
5. Publish through a reviewed merge; never sync an unrestricted private directory.

## Corrections and removals

Public Git history and Arweave data may remain available after deletion. If sensitive information is published, rotate or revoke the affected secret first, then remove it from current content and repository history where feasible.
