# dolifer / claude-plugins

A [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) hosting plugins maintained by [@dolifer](https://github.com/dolifer).

## Install

```
/plugin marketplace add dolifer/claude-plugins
```

## Available plugins

| Plugin | Channel | Purpose |
|---|---|---|
| `ngql` | stable | NGql Claude Code Skill, tracking the current stable [NGql.Core](https://www.nuget.org/packages/NGql.Core) release. |
| `ngql-preview` | preview | NGql Skill tracking the latest preview release. May reference library APIs that have not yet shipped to stable. |

Install one or both:

```
/plugin install ngql@dolifer            # stable
/plugin install ngql-preview@dolifer    # preview
```

Both plugins can coexist in the same Claude Code session — they're invoked via `/ngql:<skill>` and `/ngql-preview:<skill>` respectively.

## Update

```
/plugin marketplace update
```

## How releases land here

This repository receives commits from automated `make skill-publish-{preview,stable}` runs in [dolifer/NGql](https://github.com/dolifer/NGql). Manual edits are usually unnecessary; if a plugin's `SKILL.md` content needs to change, the source-of-truth lives at `dolifer/NGql:.claude/skills/ngql-local/SKILL.md`.

## License

The plugin contents are individually licensed (each plugin folder has its own LICENSE). The catalog manifest is MIT.
