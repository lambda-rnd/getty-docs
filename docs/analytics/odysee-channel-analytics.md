# Odysee channel analytics

**Status:** Concept · **Audience:** Odysee creators and researchers

Getty can present analytics for an authorized Odysee channel without making the administrative data source a public API.

## Channel overview

An overview can include:

- Published video count.
- Channel views and subscribers.
- Likes and dislikes when supplied by the data source.
- Time-bucketed video and view activity.
- Changes relative to an earlier comparable period.
- All-time, recently published, or most-commented content highlights.

Supported reporting ranges can include a day, week, month, six months, or year. A comparison value depends on the selected range and available historical data.

## Content detail

Individual content summaries can include views, fire and slime reactions, comments, publication growth, and support amount and currency when available. A support value is a provider-derived metric and should not be interpreted as a settled wallet balance.

## Authorization boundary

Channel analytics shown in getty admin are owner-authorized views. Their presence in the product does not make the underlying administrative routes, tokens, or ownership checks public integration contracts.

Public examples must use fictional channels, claim IDs, titles, thumbnails, and support values.

---

[Previous: Platform comparison](platform-comparison.md) · [Analytics index](index.md) · [Next: Twitch and Kick activity](twitch-kick-activity.md)
