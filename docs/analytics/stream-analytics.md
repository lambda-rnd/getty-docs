# Stream analytics

**Status:** Concept · **Audience:** Streamers and analytics consumers

Getty records periodic observations while a stream is live. Session and daily summaries are derived from those observations, so they can differ from final reports produced by a streaming platform.

## Core metrics

| Metric                           | Derivation                                                     | Important limitation                                                           |
| -------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Duration                         | Elapsed observed live time                                     | Brief disconnects or delayed state changes can affect boundaries               |
| Average viewers                  | Viewer-seconds divided by observed live seconds                | Accuracy depends on sampling coverage                                          |
| Peak viewers                     | Maximum concurrent-viewer sample                               | It is not a unique-viewer count                                                |
| Viewer hours                     | Viewer-seconds divided by 3,600                                | It is an approximation between samples                                         |
| Active days                      | Reporting days containing live activity                        | Day boundaries depend on the reporting timezone                                |
| Followers gained                 | Sum of positive differences between follower samples           | Unfollows and provider corrections can make this differ from a provider report |
| Session chatters (range maximum) | Highest distinct-chatter count recorded for one stream session | It does not deduplicate or add chatters across multiple sessions               |
| Tips                             | Recorded tip count and value for the relevant period           | Currency conversions are reference estimates, not accounting statements        |

## Cross-platform viewers

When multiple providers are enabled, getty can add the current Odysee, Twitch, and Kick viewer samples. This produces a useful operational total, but it does not identify or deduplicate people across platforms.

For example, a viewer watching the same stream on Odysee and Twitch contributes to both platform samples. The combined value should therefore be labeled “cross-platform viewers” or “combined concurrent viewers,” not “unique viewers.”

## Sessions and reporting buckets

A stream session describes one observed live interval. Longer reports group activity into calendar buckets and can include streamed hours, average viewers, peak viewers, follower changes, chatter activity, and tips. When a range contains multiple sessions, the chatter value is the largest per-session distinct count, not a range-wide distinct-user total.

Aggregating daily summaries again can lose detail. Consumers should use the most granular supported data when they need to reproduce a calculation.

## Appropriate uses

These metrics are suitable for creator dashboards, relative trend comparisons, overlay status, and operational summaries. They should not be treated as audited advertising impressions, billing records, or proof of a specific person's attendance.

---

[Previous: Analytics glossary](glossary.md) · [Analytics index](index.md) · [Next: Platform comparison](platform-comparison.md)
