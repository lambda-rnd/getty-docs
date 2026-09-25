# Documentation style guide

**Status:** Stable policy · **Audience:** Contributors

Use this guide to keep getty documentation clear, consistent, and portable between GitHub and the getty blog.

## Core principles

- Lead with the reader outcome.
- Separate supported contracts from concepts and observations.
- Prefer plain language, short sections, and precise definitions.
- Use only information approved for public documentation.
- Keep Markdown portable; presentation must not depend on a dedicated documentation site.

## Page structure

Documentation pages should normally follow this order:

1. One level-one title.
2. A compact metadata line with status and audience.
3. A short paragraph explaining the page outcome.
4. Sections ordered from common use to deeper reference.
5. A divider and links back to an index or adjacent page.

Use this metadata format:

```md
**Status:** Concept · **Audience:** Developers and researchers
```

## Status labels

| Label | Use |
| --- | --- |
| **Stable** | Supported public contract or policy |
| **Preview** | Public behavior that can still change |
| **Concept** | Explanation that does not guarantee an API or payload |

Do not imply stability through wording alone. A contract is stable only when its page explicitly says so.

## Brand and terminology

- Write `getty` in lowercase within sentences.
- `Getty` is acceptable at the beginning of a paragraph, sentence, or list item.
- Preserve the official spelling of AO, Arweave, HyperBEAM, Odysee, Twitch, Kick, YouTube, OBS, KICKs, and Permaweb.
- Define getty-specific or platform-specific terminology on first use.
- Do not describe peak or sampled values as unique users unless the contract truly measures distinct identities.

## Visual patterns

- Use tables for comparisons and exact mappings, not for long prose.
- Use GitHub-style callouts sparingly for important notes, warnings, or contract boundaries.
- Use Mermaid only when a relationship is materially clearer as a diagram.
- Use fenced code blocks for payloads, paths, and commands.
- Use `<details>` only for optional, lengthy material and verify that the blog renderer supports it before copying.
- Avoid decorative badge walls, repeated emojis, raw HTML layout, and images without informational value.

## Links and navigation

- Prefer relative links for repository content.
- Give links descriptive labels; avoid “click here.”
- End documentation pages with a small set of useful navigation links.
- Check links after moving or renaming a page.
- Treat tokenized URLs and public identifiers as correlatable data; examples must remain synthetic.

## Examples and schemas

- Use obviously fictional values.
- Keep examples minimal while still valid against their documented schema.
- State whether an example is conceptual or a supported contract.
- Do not extend a public schema merely to describe internal or temporary state.

## Reuse in the blog

The repository is the versioned source; the blog is the presentation layer. Blog copies can add introductions, screenshots, or reader-oriented tutorials, but technical definitions and supported contracts should remain consistent with this repository.

When the blog renderer differs from GitHub, adapt presentation syntax without changing the documented meaning.

## Review checklist

- The status and audience are present.
- The outcome is clear in the opening paragraph.
- Terminology follows the brand rules.
- Examples are synthetic and contain no private data.
- Links and schemas validate.
- The change does not expose non-public implementation or operational details.

---

[Repository overview](README.md) · [Contributing](CONTRIBUTING.md) · [Publication policy](PUBLICATION_POLICY.md)
