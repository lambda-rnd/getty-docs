# Architecture

**Status:** Concept · **Audience:** Developers and researchers

Getty separates public presentation, hosted coordination, permanent storage, and decentralized compute. Deployments can enable only the components they need.

```mermaid
flowchart LR
    Operator[Streamer / operator] --> Admin[getty admin]
    Viewer[Viewer] --> Platform[Streaming platform]
    Platform --> Hosted[getty hosted services]
    Admin --> Hosted
    Hosted --> Overlay[OBS overlay]
    Hosted -- archives and public assets --> Arweave[Arweave permanent data]
    Hosted -- authorized signed messages --> AO[AO network processes]
    AO -- materialized state --> HyperBEAM[HyperBEAM read interface]
    Arweave -- Permaweb entry or archive --> Overlay
    HyperBEAM -- state reads --> Hosted
```

## Responsibilities

- **Getty admin** manages user-authorized configuration and actions.
- **Hosted services** coordinate authenticated writes, public read models, WebSocket updates, and compatibility fallbacks.
- **OBS overlays** render public presentation state and must not receive private wallet material.
- **Arweave** stores immutable assets, selected result records, and verified archives.
- **AO** provides network-resident state and computation for supported modules; it does not run as an application-server daemon.
- **HyperBEAM** materializes selected AO process state through HTTP-readable interfaces.

## Trust boundary

Public widget tokens and URLs are designed for presentation and read access. They are not administrative credentials. Wallet signing material, private tenant mappings, and write authorization remain outside public overlays.

> [!IMPORTANT]
> getty keeps process ownership, application signing, and tenant storage authorization as separate roles. Browsers and overlays receive public results and read models, never private wallet keys.

---

[Documentation index](index.md) · [Next: Overlays and OBS](overlays.md)
