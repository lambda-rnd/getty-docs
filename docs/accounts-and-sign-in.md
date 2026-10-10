# Accounts and sign-in

**Status:** Concept · **Audience:** Streamers and account owners

Getty separates the method used to enter a workspace from the accounts connected to its streaming tools. Sign-in with Twitch or Kick and explicit Stream History source selection depend on deployment availability.

## Sign-in, verification, and connections

| Action                        | Purpose                                                                                | What it does not imply                                                   |
| ----------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Sign in                       | Enter the workspace associated with a verified identity                                | Enable chat, notifications, or history collection                        |
| Verify an account             | Explicitly associate a provider identity with the current workspace for account access | Replace an existing tool connection or transfer another workspace's data |
| Connect chat or notifications | Authorize the applicable streaming feature                                             | Automatically make that account a Getty sign-in method                   |
| Select a history source       | Include a supported connected channel in future observations                           | Import all provider analytics or reconstruct earlier streams             |

The Accounts section in Settings brings these states together and provides links to the relevant feature settings. An account can be verified for access while its chat or notifications are disconnected, or connected to a tool without being verified for sign-in.

Provider identities follow the provider's account identifier rather than a display name. Renaming a channel does not, by itself, create a new Getty workspace. Getty's own account access controls still apply when a provider is used to sign in.

## Keep an existing workspace

If you already use Getty, sign in with your usual method and verify the additional account from that workspace's settings when the option is available. A verified additional sign-in method preserves the workspace and its data.

Creating a separate workspace does not merge it with an older one. Matching names or email addresses are not evidence that two workspaces should be combined. Account verification is not a workspace consolidation procedure; use the deployment's support process if an identity is already associated with another workspace.

Changing the sign-in method does not itself replace configurations, widget access, stream history, or the configured storage wallet. Treat full widget URLs and workspace identifiers as private account configuration.

## Storage wallets are separate

An Odysee, Twitch, or Kick identity is an access method. An Arweave storage wallet authorizes permanent publication for the configured data owner. Signing in with a platform does not automatically create a storage wallet or authorize spending.

Where wallet setup is available, creating or importing a storage wallet does not change the workspace identity or the current sign-in method. Keep any wallet backup private. Replacing a wallet requires its own confirmation and resets paid-media authorization to Free only.

Existing permanent archives retain their original publication owner. Replacing the current wallet does not rewrite those records or transfer ownership of previously published content. See [permanent storage](ao-arweave-hyperbeam.md#stream-history-archives) for the distinction between live data and verified archives.

## Availability

Use the options actually shown by the deployment. A provider connection does not guarantee that provider sign-in, every permission, or every history metric is available. Features under evaluation may remain disabled while existing access continues to work.

---

[Documentation index](index.md) · [Architecture](architecture.md) · [Stream analytics](analytics/stream-analytics.md)
