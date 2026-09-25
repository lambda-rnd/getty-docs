# Analytics

**Status:** Concept · **Audience:** Streamers, integrators, and researchers

Getty combines observations from streaming platforms with locally recorded activity. These pages explain what the resulting metrics mean, where they come from, and which limitations apply. They do not expose administrative API contracts.

## Documentation map

| Topic                                                 | Document                                                |
| ----------------------------------------------------- | ------------------------------------------------------- |
| Metric names and common terms                         | [Glossary](glossary.md)                                 |
| Stream duration, viewers, followers, and chatters     | [Stream analytics](stream-analytics.md)                 |
| Differences between Odysee, Twitch, and Kick          | [Platform comparison](platform-comparison.md)           |
| Odysee channel and content metrics                    | [Odysee channel analytics](odysee-channel-analytics.md) |
| Twitch and Kick activity events                       | [Twitch and Kick activity](twitch-kick-activity.md)     |
| Normalized chat data and safe aggregates              | [Chat data](chat-data.md)                               |
| Timestamps, stale data, missing values, and estimates | [Data freshness and quality](data-freshness.md)         |

## Interpretation principles

- A displayed metric can be sampled, event-derived, or fetched from a provider API.
- Cross-platform totals are sums, not deduplicated audience measurements.
- Missing data is different from a measured value of zero.
- Historical activity begins when collection is enabled and is not necessarily retroactive.
- Provider dashboards can differ because their aggregation windows, filtering, and late corrections are not identical to getty's.

No page in this section makes an undocumented administrative endpoint a supported public API.

---

[Documentation index](../index.md) · [Next: Analytics glossary](glossary.md)
