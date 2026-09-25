# Overlays and OBS

**Status:** Preview · **Audience:** Streamers and operators

Getty overlays are browser sources that present stream activity. A deployment can provide hosted overlay URLs and, for supported widgets, a Permaweb entry point.

## Typical setup

1. Open the relevant module in getty admin.
2. Copy the generated widget URL.
3. Add it to OBS as a Browser Source.
4. Preserve the full URL and treat embedded tokens as private-to-the-stream configuration.
5. Test the overlay before going live.

## Hosted and Permaweb entry points

- A **hosted** overlay loads its document and runtime assets from getty.
- A **Permaweb** overlay can load an immutable entry document from Arweave while still using supported getty services for live state.

The availability of a Permaweb URL does not imply that every piece of live state is stored permanently.

## Supported overlay families

Getty can expose overlays for chat, polls, raffles, achievements, alerts, goals, recent activity, and other stream presentation modules. Availability depends on the getty deployment and enabled modules.

## Safety

Do not publish complete widget URLs in screenshots, issues, or examples. Use placeholders such as:

```text
https://<getty-host>/widgets/polls?token=<public-token>
```

---

[Previous: Architecture](architecture.md) · [Documentation index](index.md) · [Next: AO, Arweave, and HyperBEAM](ao-arweave-hyperbeam.md)
