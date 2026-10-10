# Twitch and Kick activity

**Status:** Concept · **Audience:** Twitch and Kick creators

Getty can retain selected Twitch and Kick activity events after the corresponding provider is connected and history collection is enabled.

## Historical metrics

Depending on provider support, summaries can include:

- Followers gained.
- New and renewed subscriptions.
- Gifted subscriptions.
- Twitch Bits or gifted KICKs.
- Raids and reported raid viewers.

Week, month, and year views describe getty's retained event window. They are not guaranteed to reproduce the provider's own analytics dashboard.

## Activity events and audience observations

Activity history and Stream History source selection serve different purposes. A follow, subscription, gift, or raid event is not a periodic viewer sample and cannot reconstruct a missing audience curve. Provider sign-in does not by itself enable either form of collection.

The observed-source history view reports supported audience observations and collection coverage; it does not promise all native follower, subscription, or revenue metrics. Keep AR tips, Twitch Bits, KICKs, and subscriptions in their own units rather than adding them into one revenue total.

## Current state

Current follower or active-subscriber counts can be fetched separately from historical activity. Twitch may also expose a creator goal with a type, description, current value, and target. Current state can remain useful even when historical persistence is unavailable.

## History boundary

Historical tracking is not retroactive. `trackingSince` identifies the earliest known point from which getty retained the applicable provider activity. Events before that point must not be inferred as zero.

Synthetic, test, or preview events are not part of production analytics and should not be counted in published examples.

---

[Previous: Odysee channel analytics](odysee-channel-analytics.md) · [Analytics index](index.md) · [Next: Chat data](chat-data.md)
