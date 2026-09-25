# Chat data

**Status:** Concept · **Audience:** Streamers and integrators

Getty normalizes presentation fields from supported chat providers so overlays and dashboards can render a consistent message shape. Depending on deployment and account configuration, chat sources can include Odysee, Twitch, Kick, and YouTube. Provider-specific capabilities remain optional.

Chat-provider support is separate from stream-viewer aggregation. A provider can supply chat messages without participating in the combined Odysee, Twitch, and Kick viewer count.

## Normalized presentation fields

A normalized chat message can contain:

- Source platform.
- Display name or channel name.
- Avatar URL when available.
- Message text and timestamp.
- Provider badges, emotes, or moderator state when available.

The absence of a badge, avatar, emote, or moderation flag is not necessarily an error. Providers expose different fields and can change their payloads.

## Safe aggregate analytics

Public documentation and synthetic examples can describe:

- Message count and messages per minute.
- Active chatter counts or per-session distinct-chatter counts with a precise definition.
- Activity by reporting period.
- Aggregate share of messages by platform.
- Aggregate command usage when it cannot identify a user.

## Privacy boundary

Chat text, display names, avatars, timestamps, and provider identifiers can be personal or correlatable data even when visible on a public stream. Public documentation must not contain real transcripts, production usernames, avatar URLs, user identifiers, moderation records, or cross-platform identity mappings.

Any future public chat schema must minimize identity fields, define retention expectations, and use entirely synthetic examples. A normalized internal representation is not automatically a supported public API contract.

---

[Previous: Twitch and Kick activity](twitch-kick-activity.md) · [Analytics index](index.md) · [Next: Data freshness and quality](data-freshness.md)
