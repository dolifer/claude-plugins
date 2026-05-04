---
layout: default
title: dolifer / claude-plugins
description: Claude Code plugin marketplace — Skills authored by Denis Olifer.
---

A [Claude Code](https://docs.claude.com/en/docs/claude-code) plugin marketplace maintained by **[@dolifer](https://github.com/dolifer)**. Each plugin below has its own page with install instructions, version, and details.

---

## Add the marketplace

Inside any Claude Code session:

```text
/plugin marketplace add dolifer/claude-plugins
```

Then install whichever plugins you want from the table below. To pull updates later:

```text
/plugin marketplace update
```

---

## Available plugins

<table class="plugins-table">
  <thead>
    <tr>
      <th>Plugin</th>
      <th>Status</th>
      <th>Latest published</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    {% assign sorted = site.skills | sort: 'order' %}
    {% for skill in sorted %}
      {% assign data = site.data.plugins[skill.name] %}
      <tr>
        <td>
          <a href="{{ skill.url | relative_url }}"><code>{{ skill.name }}</code></a>
        </td>
        <td>
          <span class="status status-{{ skill.status }}">
            {%- if skill.status == 'live' -%}live
            {%- elsif skill.status == 'coming-soon' -%}coming soon
            {%- elsif skill.status == 'deprecated' -%}deprecated
            {%- else -%}{{ skill.status }}
            {%- endif -%}
          </span>
        </td>
        <td>
          {%- if data.version and data.version != '0.0.0' -%}
            <code>{{ data.version }}</code>
          {%- else -%}
            <em>—</em>
          {%- endif -%}
        </td>
        <td>{{ skill.description }}</td>
      </tr>
    {% endfor %}
  </tbody>
</table>

---

## Reporting issues

- **Per-plugin issues** (wrong example, hallucinated method, broken auto-trigger) — open the plugin's page above and use the issue-tracker link there. Each plugin's content is generated from its source repo, so the bug lives there, not here.
- **Catalog issues** (install fails, marketplace not loading, version pinning issues, this Pages site itself) — file in [dolifer/claude-plugins/issues](https://github.com/dolifer/claude-plugins/issues).

---

## License

Each plugin entry inside this catalog declares its own `license`. The catalog manifest is MIT.

<style>
  .status {
    display: inline-block;
    padding: 2px 10px;
    border-radius: 12px;
    font-size: 0.85em;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .status-live { background: #2ea44f; color: #fff; }
  .status-coming-soon { background: #d29922; color: #fff; }
  .status-deprecated { background: #6e7781; color: #fff; }
  table { width: 100%; }
  td code, th code { font-size: 0.95em; }
  /* Keep Plugin (col 1) and Status (col 2) on a single line — Cayman's default
     auto-layout shrinks them and wraps "ngql-preview" or the "coming soon" pill
     onto two lines. Description (col 4) absorbs the freed width. Scoped to the
     plugins table so future markdown tables on this page aren't affected. */
  .plugins-table th:nth-child(1), .plugins-table td:nth-child(1),
  .plugins-table th:nth-child(2), .plugins-table td:nth-child(2) {
    white-space: nowrap; width: 1%;
  }
</style>
