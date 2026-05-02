---
layout: skill
name: ngql
title: "ngql — Stable build of the NGql Skill"
description: >
  Stable Claude Code Skill for the NGql query builder, tracking the current released
  NGql.Core version. Pairs with the `dotnet-ngql` CLI for verifying generated snippets.
channel: stable
status: coming-soon
plugin_install: /plugin install ngql@dolifer
invoke: /ngql:ngql
companion_tool:
  name: dotnet-ngql
  url: https://www.nuget.org/packages/dotnet-ngql/
  install: dotnet tool install -g dotnet-ngql
order: 1
---

The stable channel of the NGql Claude Code Skill. Will track each `NGql.Core` stable release once `2.1.0` (or the next stable) ships to NuGet.

Until then, install the [preview channel](/skills/ngql-preview/) to use the Skill — preview content is otherwise identical, just versioned by commit count rather than by release tag.

### When stable will publish

Stable releases happen on `skill-v<X.Y.Z>` git tags pushed to [`dolifer/NGql`](https://github.com/dolifer/NGql), which triggers the `release-skill.yml` workflow. The first stable release is gated on confirming the Skill content has stabilized in preview — once SKILL.md edits stop happening every other day, the preview promotes to stable.

### Same plugin shape, side-by-side install

Once stable ships, you can have **both** channels installed in the same Claude Code session: `/ngql:ngql` invokes stable, `/ngql-preview:ngql` invokes preview. Useful for comparing behavior between channels or A/B-ing a Skill change before promoting it.
