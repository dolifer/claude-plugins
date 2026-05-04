---
layout: skill
name: ngql-preview
title: "ngql-preview — Preview build of the NGql Skill"
description: >
  Author NGql query-builder C# in Claude Code — from natural language, paste,
  or curl. Pairs with the `dotnet-ngql` CLI to verify rendered GraphQL. Preview
  channel, tracks every push to `main` and may reference unreleased library APIs.
channel: preview
status: live
plugin_install: /plugin install ngql-preview@dolifer
invoke: /ngql-preview:ngql
companion_tool:
  name: dotnet-ngql
  url: https://www.nuget.org/packages/dotnet-ngql/
  install: dotnet tool install -g dotnet-ngql --prerelease
issues:
  url: https://github.com/dolifer/NGql/issues
  label: skill
order: 2
---

### What is NGql?

NGql is a **zero-dependency, schema-less GraphQL query builder for .NET**. Compose queries and mutations from C# with a fluent API — no SDL, no codegen, no schema validation step. Multi-targets `net8.0` / `net9.0` / `net10.0`.

The library is fully usable on its own. To track the preview channel matching this Skill, pin a preview version:

```bash
dotnet add package NGql.Core --version 2.1.1-preview.X
```

Or skip `--version` to get the latest stable.

Library docs: [dolifer.github.io/NGql/](https://dolifer.github.io/NGql/) · Source: [github.com/dolifer/NGql](https://github.com/dolifer/NGql)

### What this Skill is for

This Skill is a productivity layer on top of the library. It teaches Claude Code to translate your intent — natural language, pasted GraphQL, or a curl command — into NGql query-builder C# code, and (when explicitly asked) to verify the rendered GraphQL via the `dotnet-ngql` CLI before you commit. Use it when you want Claude to author NGql code; skip it when you'd rather write the C# yourself.

The preview channel may reference library APIs that haven't shipped to stable yet — useful for testing upcoming NGql changes or comparing behavior against stable side-by-side.

Three modes:

1. **Natural language → builder.** *"Get the top 10 repos of GitHub user dolifer with stargazer counts."* → a `QueryBuilder.CreateDefaultBuilder(...)` snippet using the fluent API.
2. **GraphQL or curl → builder.** Paste an operation or curl command, the Skill rewrites it as NGql calls — preserving operation name, variable types, enum literals, nested arguments, and inline fragments via `OnType`.
3. **Refactor / preserve.** *"Strip `ssn` and `email` from this builder."* → a `PreservationBuilder.Preserve(...)` chain that keeps everything else.

The Skill is **prescriptive** — it picks one safe API idiom per situation and refuses to generate code for unsupported GraphQL constructs (named fragments, directives, subscriptions). When the request needs something NGql can't model, the Skill stops, surfaces the gap, and offers concrete workaround paths instead of producing broken code with a warning.

Pairs with the `dotnet-ngql` CLI to verify rendered GraphQL — the Skill produces the snippet and command line, and (when explicitly asked) runs the tool for you, surfacing the rendered GraphQL and any execution result.

### Updating

Pull the latest preview into your Claude Code session:

```text
/plugin marketplace update
/plugin update ngql-preview@dolifer
/reload-plugins
```

### Switching to stable

The [stable `ngql` channel](/skills/ngql/) is also live — both can coexist in the same Claude Code session. Invoke as `/ngql:ngql` (stable) vs `/ngql-preview:ngql` (preview). Preview is allowed to break and iterate; stable carries SemVer guarantees and ships only on `skill-v<X.Y.Z>` tags.
