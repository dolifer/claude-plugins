---
layout: skill
name: ngql
title: "ngql — Stable build of the NGql Skill"
description: >
  Stable Claude Code Skill for the NGql query builder, paired with the released
  NGql.Core version on NuGet. Pairs with the `dotnet-ngql` CLI for verifying
  generated snippets against a real or local endpoint.
channel: stable
status: live
plugin_install: /plugin install ngql@dolifer
invoke: /ngql:ngql
companion_tool:
  name: dotnet-ngql
  url: https://www.nuget.org/packages/dotnet-ngql/
  install: dotnet tool install -g dotnet-ngql
issues:
  url: https://github.com/dolifer/NGql/issues
  label: skill
order: 1
---

The Skill teaches Claude to author NGql query-builder C# from natural language, pasted GraphQL operations, or curl commands. Three modes:

1. **Natural language → builder.** *"Get the top 10 repos of GitHub user dolifer with stargazer counts."* → a `QueryBuilder.CreateDefaultBuilder(...)` snippet using the fluent API.
2. **GraphQL or curl → builder.** Paste an operation or curl command, the Skill rewrites it as NGql calls — preserving operation name, variable types, enum literals, nested arguments, and inline fragments via `OnType`.
3. **Refactor / preserve.** *"Strip `ssn` and `email` from this builder."* → a `PreservationBuilder.Preserve(...)` chain that keeps everything else.

The Skill is **prescriptive** — it picks one safe API idiom per situation and refuses to generate code for unsupported GraphQL constructs (named fragments, directives, subscriptions). When the request needs something NGql can't model, the Skill stops, surfaces the gap, and offers concrete workaround paths instead of producing broken code with a warning.

Pairs with the `dotnet-ngql` CLI to verify rendered GraphQL — the Skill produces the snippet and command line, and (when explicitly asked) runs the tool for you, surfacing the rendered GraphQL and any execution result.

### Stable vs preview

This is the **stable** channel — versioned by `skill-v<X.Y.Z>` tags pushed to [`dolifer/NGql`](https://github.com/dolifer/NGql), released alongside `NGql.Core` stable releases. SemVer guarantees apply.

The [preview channel](/skills/ngql-preview/) tracks every push to `main` and may reference unreleased library APIs. Useful for testing upcoming NGql changes; not recommended for daily work.

Both channels can coexist in the same Claude Code session — `/ngql:ngql` invokes stable, `/ngql-preview:ngql` invokes preview. Pick stable for predictable behavior, preview to ride the latest.

### Updating

Pull the latest stable into your Claude Code session:

```text
/plugin marketplace update
/plugin update ngql@dolifer
/reload-plugins
```
