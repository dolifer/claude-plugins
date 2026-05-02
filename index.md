---
layout: default
title: dolifer / claude-plugins
description: Claude Code plugin marketplace — ngql + ngql-preview Skills for the NGql query builder.
---

A [Claude Code](https://docs.claude.com/en/docs/claude-code) plugin marketplace maintained by **[@dolifer](https://github.com/dolifer)**. Hosts the NGql Skill across two channels: stable and preview.

---

## Install

Inside any Claude Code session:

```text
/plugin marketplace add dolifer/claude-plugins
```

Then install whichever channel(s) you want:

```text
/plugin install ngql@dolifer            # stable
/plugin install ngql-preview@dolifer    # preview
```

Both channels can coexist. Invoke each via its plugin namespace: `/ngql:<skill>` or `/ngql-preview:<skill>`.

To pull updates later:

```text
/plugin marketplace update
```

---

## Plugins

### `ngql` — stable

Generates [NGql](https://github.com/dolifer/NGql) query-builder C# from natural language, pasted GraphQL operations, or curl commands. Pairs with the [`dotnet-ngql`](https://www.nuget.org/packages/dotnet-ngql) CLI for live verification of rendered GraphQL.

- **Tracks**: the current stable [NGql.Core](https://www.nuget.org/packages/NGql.Core) release.
- **Source of truth**: [`dolifer/NGql`](https://github.com/dolifer/NGql) at `.claude/skills/ngql-local/SKILL.md`.
- **Best for**: production code that depends on a released NGql version.

### `ngql-preview` — preview

Same Skill, but tracking the latest preview release of NGql. May reference library APIs that have not yet shipped to stable.

- **Tracks**: the most recent NGql preview tag (e.g. `2.1.0-preview.4`).
- **Best for**: testing upcoming NGql changes; comparing behavior against the stable channel side-by-side.

---

## Companion tools

The marketplace doesn't carry the library itself — these are separate packages from the same `dolifer/NGql` repository:

| Package | Purpose | Install |
|---|---|---|
| [`NGql.Core`](https://www.nuget.org/packages/NGql.Core) | The query-builder library. | `dotnet add package NGql.Core` |
| [`dotnet-ngql`](https://www.nuget.org/packages/dotnet-ngql) | CLI that renders a `QueryBuilder` snippet to GraphQL and optionally executes it against a live endpoint. | `dotnet tool install -g dotnet-ngql` |

Use the CLI to verify Skill-generated code without leaving your terminal:

```bash
echo 'QueryBuilder.CreateDefaultBuilder("Hello").AddField("world.name")' | ngql
# → query Hello{
#       world{
#           name
#       }
#   }
```

---

## How it works

| Layer | Lives in |
|---|---|
| Skill source-of-truth | [`dolifer/NGql:.claude/skills/ngql-local/SKILL.md`](https://github.com/dolifer/NGql/blob/main/.claude/skills/ngql-local/SKILL.md) |
| Per-channel build script | [`dolifer/NGql:.claude/skills/ngql-local/scripts/stage_skill.py`](https://github.com/dolifer/NGql/blob/main/.claude/skills/ngql-local/scripts/stage_skill.py) |
| Catalog manifests + per-channel content (this repo) | [`dolifer/claude-plugins`](https://github.com/dolifer/claude-plugins) |

A `make skill-publish-{preview,stable}` target in `dolifer/NGql` stages the Skill, rewrites its frontmatter for the target channel, bumps the channel's `plugin.json` version, and commits to this repo. End users only ever interact with `/plugin marketplace add dolifer/claude-plugins`.

---

## Report issues

- **Skill content** (wrong example, hallucinated method, broken auto-trigger): file in [dolifer/NGql/issues](https://github.com/dolifer/NGql/issues) with the `skill` label. The Skill content is generated from `dolifer/NGql`; a fix lands here automatically on the next release.
- **Catalog manifest** (install fails, marketplace not loading, version pinning issues): file in [dolifer/claude-plugins/issues](https://github.com/dolifer/claude-plugins/issues).

---

## License

Each plugin entry inside this catalog declares its own `license`. The catalog manifest itself is MIT.
