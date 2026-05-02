---
layout: skill
name: ngql-preview
title: "ngql-preview — Preview build of the NGql Skill"
description: >
  Tracks the latest preview release of NGql. Content here may reference library APIs
  that haven't shipped to the stable `ngql` channel yet — install this if you're testing
  upcoming NGql changes or comparing behavior against stable side-by-side.
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

The Skill teaches Claude to author NGql query-builder C# from natural language, pasted GraphQL operations, or curl commands. Three modes:

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

Once the stable `ngql` channel publishes, both can coexist — invoke as `/ngql:ngql` (stable) vs `/ngql-preview:ngql` (preview) without conflict. Preview is allowed to break and iterate; stable carries SemVer guarantees.
