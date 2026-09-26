# getty docs

Public, implementation-neutral documentation intended for streamers, integrators, developers, and researchers who use getty.

> [!IMPORTANT]
> This repository is the public, versioned source for getty technical documentation. Content becomes a supported public contract only when a page explicitly says so.

## Choose a path

| Learn                                                      | Build                                      | Verify                                               |
| ---------------------------------------------------------- | ------------------------------------------ | ---------------------------------------------------- |
| [Architecture](docs/architecture.md)                       | [Overlays and OBS](docs/overlays.md)       | [Security and privacy](docs/security-and-privacy.md) |
| [Analytics](docs/analytics/index.md)                       | [Supported public API](docs/public-api.md) | [Publication policy](PUBLICATION_POLICY.md)          |
| [AO, Arweave, and HyperBEAM](docs/ao-arweave-hyperbeam.md) | [Schemas and examples](schemas/README.md)  | [Contribution guide](CONTRIBUTING.md)                |

For the complete map, start with the [documentation index](docs/index.md).

## Public data artifacts

- [`schemas/`](schemas/README.md) contains machine-readable public payload contracts.
- [`examples/`](examples/README.md) contains synthetic examples with no production identifiers.

## Document status

| Label       | Meaning                                        |
| ----------- | ---------------------------------------------- |
| **Stable**  | Supported public policy or contract            |
| **Preview** | Available for evaluation and subject to change |
| **Concept** | Explanatory material, not an API guarantee     |

## Scope

This repository explains public behavior and stable integration contracts. It intentionally excludes private source code, administrative APIs, deployment topology, credentials, tenant identifiers, operational logs, and incident details.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request. Security reports must follow [SECURITY.md](SECURITY.md) and must not be submitted as public issues.

## License

Documentation, including Markdown files, diagrams, and documentation media, is licensed under [CC BY 4.0](LICENSES/CC-BY-4.0.txt).

When reusing documentation, attribute “getty Docs contributors,” link to the source repository, identify the CC BY 4.0 license, and indicate whether changes were made.

JSON schemas, executable examples, scripts, configuration, and source code are licensed under [Apache License 2.0](LICENSES/Apache-2.0.txt). See [LICENSE](LICENSE) for the complete scope.

The licenses do not grant permission to use the getty name or visual identity to imply endorsement, sponsorship, or official status.
