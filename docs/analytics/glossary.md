# Analytics glossary

**Status:** Concept · **Audience:** All analytics readers

Use this glossary to distinguish sampled values, event-derived metrics, and provider totals before comparing reports.

## Stream metrics

| Term                             | Meaning                                                                                                                         |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Current viewers                  | Most recent available concurrent-viewer sample for a live platform                                                              |
| Cross-platform viewers           | Sum of the current live samples from enabled providers; one person watching on multiple platforms can be counted more than once |
| Average viewers                  | Time-weighted average of the available viewer samples during a stream                                                           |
| Peak viewers                     | Highest concurrent-viewer sample observed during a stream or reporting bucket                                                   |
| Streamed hours                   | Time during which the stream was observed as live                                                                               |
| Viewer hours                     | Approximate area under the concurrent-viewer curve, expressed in hours                                                          |
| Active day                       | A calendar day containing recorded live activity, interpreted using the configured reporting timezone                           |
| Followers gained                 | Positive follower-count changes observed during a reporting period                                                              |
| Session chatters (range maximum) | Highest distinct-chatter count recorded for one stream session in the reporting range                                           |

“Peak viewers” must not be described as “unique viewers.” A concurrent peak does not reveal how many distinct people watched over the entire stream. A range-level chatter maximum describes the largest recorded session; it is not the number of distinct people across every session in the range.

## Platform activity

| Term                | Meaning                                                                           |
| ------------------- | --------------------------------------------------------------------------------- |
| New subscription    | Subscription-start event recorded after activity tracking began                   |
| Renewal             | Recorded continuation or resubscription event                                     |
| Gifted subscription | Subscription credited as a gift by the provider event                             |
| Bits                | Twitch cheering units reported by Twitch events                                   |
| KICKs gifted        | KICKs amount reported by Kick gift events                                         |
| Raid                | Provider event that transfers or directs an audience to a channel                 |
| Tracking since      | Earliest known time from which getty has retained the applicable activity history |

## Availability terms

| Value or label        | Meaning                                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------------------- |
| `0`                   | The metric was available and its measured value was zero                                                 |
| `null` or unavailable | The provider did not supply a usable value, the account was not connected, or collection was unavailable |
| Stale                 | A previous valid snapshot is being shown because a newer fetch could not be completed                    |
| Estimated             | The value was derived from samples or deltas rather than supplied as a final provider total              |

---

[Analytics index](index.md) · [Next: Stream analytics](stream-analytics.md)
