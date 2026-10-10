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

Current live displays can add available Odysee, Twitch, and Kick viewer samples. A partial current total covers only the responding sources and must not be presented as a complete historical observation. Where observed-source history is enabled, a complete combined audience value requires usable observations from all sources selected for that interval. Neither form identifies or deduplicates people across platforms.

For example, a viewer watching the same stream on Odysee and Twitch contributes to both platform samples. The combined value should therefore be labeled “cross-platform viewers” or “combined concurrent viewers,” not “unique viewers.”

## Selected sources and observed history

Where available, Stream History settings allow explicit selection of supported connected sources. A Twitch-only or Kick-only selection can collect observations without an Odysee channel. Signing in with a provider or connecting its chat does not automatically select it for history.

This observed-source view complements existing stream summaries. It can distinguish complete, partial, and unknown observations, report collection coverage, and filter by platform and channel. A confirmed live observation on at least one selected source can contribute to global observed live time; simultaneous live intervals are counted once rather than added together.

An unavailable provider response is not evidence that the stream ended and is not a measured audience of zero. Gaps remain unknown once an observation is no longer usable. Enabling a source later does not reconstruct missing observations, and older history without channel or quality information remains limited to what was originally recorded.

Follower changes, chatter metrics, tips, and provider activity have separate sources. Their presence in an existing summary does not make them available in every observed-source report. Twitch/Kick activity events are not a substitute for viewer samples; unsupported native metrics should remain unavailable.

## Sessions and reporting buckets

A stream session describes one observed live interval. Longer reports group activity into calendar buckets and can include streamed hours, average viewers, peak viewers, follower changes, chatter activity, and tips. When a range contains multiple sessions, the chatter value is the largest per-session distinct count, not a range-wide distinct-user total.

Aggregating daily summaries again can lose detail. Consumers should use the most granular supported data when they need to reproduce a calculation.

## Appropriate uses

These metrics are suitable for creator dashboards, relative trend comparisons, overlay status, and operational summaries. They should not be treated as audited advertising impressions, billing records, or proof of a specific person's attendance.

---

[Previous: Analytics glossary](glossary.md) · [Analytics index](index.md) · [Next: Platform comparison](platform-comparison.md)
