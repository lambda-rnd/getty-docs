# Data freshness and quality

**Status:** Concept · **Audience:** Analytics consumers and integrators

Analytics consumers need both a value and enough context to judge that value. Interfaces should expose an update timestamp and should distinguish a current response from a cached fallback.

## Recommended metadata

| Field or state     | Purpose                                                                      |
| ------------------ | ---------------------------------------------------------------------------- |
| `updatedAt`        | Time represented by the current summary or provider response                 |
| `fetchedAt`        | Time at which getty obtained the displayed snapshot                          |
| `stale`            | Indicates that the value is older than the preferred freshness window        |
| `cacheFallback`    | Indicates that a previous valid snapshot is shown after a newer fetch failed |
| `trackingSince`    | Beginning of retained event history for the applicable provider              |
| Availability state | Distinguishes a measured value from a missing provider response              |

Names in this table describe concepts. They are a payload contract only when a stable schema explicitly defines them.

## Missing, zero, and stale

- `0` means the metric was available and measured as zero.
- `null` or an unavailable label means no usable value was obtained.
- A stale value remains a real previous observation, but it is not a current measurement.
- A cached fallback should retain its original observation time rather than appearing newly measured.

## Observed-history coverage

Coverage describes the part of the selected source interval for which usable audience observations exist. It is not a measure of unique viewers or proof that all activity was recorded. Complete, partial, and unknown observations must remain distinguishable.

A sample cannot be extended indefinitely across an API outage. A confirmed offline observation and a failed request have different meanings: the former is an observation, while the latter leaves an unknown interval. A day without usable data should appear as a gap rather than a measured zero.

Selecting a different channel or source changes what future observations describe. Older rows and archives keep their original context; records that lack channel or quality metadata cannot be assigned that information retroactively.

## Sources of variance

Differences between getty and a provider dashboard can result from sampling intervals, reporting timezones, stream boundary detection, delayed events, provider corrections, unavailable observations, or different aggregation rules.

Trend comparisons are most reliable when the source, range, timezone, and collection method remain consistent.

---

[Previous: Chat data](chat-data.md) · [Analytics index](index.md) · [Documentation index](../index.md)
