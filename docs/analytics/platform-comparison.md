# Platform comparison

**Status:** Concept · **Audience:** Streamers and integrators

Provider capabilities and account permissions differ. A blank field can mean that a platform does not expose the value, the connected account lacks access, or the provider was temporarily unavailable.

| Capability                    | Odysee                                  | Twitch                                                       | Kick                                          |
| ----------------------------- | --------------------------------------- | ------------------------------------------------------------ | --------------------------------------------- |
| Live state                    | Supported                               | Supported when connected                                     | Supported when connected                      |
| Concurrent viewers            | Supported when available                | Supported when connected and available                       | Supported when connected and available        |
| Stream start time             | May be available                        | May be available                                             | May be available                              |
| Category                      | Provider-dependent                      | May be available                                             | May be available                              |
| Channel and content analytics | Supported for authorized channel views  | Current state and activity events                            | Current state and activity events             |
| Follow activity               | Provider-derived channel metrics        | Event history and current counts when available              | Event history when available                  |
| Subscription activity         | Not represented by the same event model | New, renewal, gift, and current-state metrics when available | Subscription and gift activity when available |
| Native engagement units       | Reactions and supports where available  | Bits                                                         | Kicks                                         |
| Raid activity                 | Not represented by the same event model | Supported when reported                                      | Supported when reported                       |

This table describes getty's conceptual data model, not every feature offered by each platform. Provider capabilities can change independently.

## Combined values

- Viewer totals are summed only from enabled, live, and available providers.
- Combined values do not perform cross-platform identity matching.
- A provider outage should produce an unavailable state rather than silently becoming a measured zero.
- Provider-specific metrics should retain their original unit and meaning instead of being forced into a misleading common total.

## Connection state

“Connected” means that a provider account or channel has been configured for the applicable feature. It does not guarantee that every metric is currently available. “Available” indicates that a usable provider response was obtained for the current observation.

---

[Previous: Stream analytics](stream-analytics.md) · [Analytics index](index.md) · [Next: Odysee channel analytics](odysee-channel-analytics.md)
