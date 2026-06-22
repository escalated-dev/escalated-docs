# Escalated Documentation

[![Docs](https://img.shields.io/badge/docs-escalated.dev-blue)](https://escalated.dev/docs)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the documentation for [Escalated](https://escalated.dev), an open-source embeddable support ticket system with SLA tracking, escalation rules, agent workflows, and a customer portal.

> **[escalated.dev/docs](https://escalated.dev/docs)** — Read the full documentation online.

The Markdown files in this repo are fetched at runtime by the Escalated marketing site and rendered as the [/docs](https://escalated.dev/docs) page.

## Structure

```
docs.json              # Manifest — defines groups, section order, sidebar labels, types, and tabs
sections/
  getting-started.md   # Single sections are standalone files
  installation/        # Tabbed sections are directories
    _intro.md          # Shared intro text (appears above the tab switcher)
    laravel.md         # One Markdown file per declared tab id
    rails.md
    ...
  compare/             # Tabs are not always frameworks — here they are competitors
    _intro.md
    zendesk.md
    freshdesk.md
    ...
```

### Manifest shape

`docs.json` is a list of **groups**; each group has a `slug`, a `label`, a `description` (shown on the
docs overview cards), and an ordered list of **sections**. Each section has a `slug` (the page URL at
`/docs/{slug}` and the content path), a `label`, and a `type`:

```json
{
  "groups": [
    {
      "slug": "getting-started",
      "label": "Getting Started",
      "description": "Install Escalated and get the support UI running in your app.",
      "sections": [
        { "slug": "getting-started", "label": "Getting Started", "type": "single" },
        {
          "slug": "installation",
          "label": "Installation",
          "type": "tabbed",
          "tabs": [
            { "id": "laravel", "label": "Laravel" },
            { "id": "rails", "label": "Rails" }
          ]
        }
      ]
    }
  ]
}
```

### Section types

- **`single`** — A standalone Markdown file (`sections/{slug}.md`) rendered as one page.
- **`tabbed`** — A directory (`sections/{slug}/`) with `_intro.md` (shared heading + intro, shown above
  the tab switcher) and one Markdown file per declared tab. The section's `tabs` array lists each tab's
  `id` (which must match a `{id}.md` file in the directory) and its `label` (shown on the switcher).
  Tabs are whatever dimension fits the section — frameworks, data sources, competitors, or topics.

## Contributing

### Editing existing docs

1. Find the section you want to edit in the `sections/` directory.
2. Edit the Markdown file directly on GitHub or clone the repo locally.
3. Open a pull request with your changes.

Changes merged to `main` will appear on the site within one hour (the cache TTL), or immediately if the cache is cleared.

### Adding a new section

1. Pick the group in `docs.json` it belongs to (or add a new group with a `slug`, `label`, and `description`).
2. Add a section entry to that group's `sections` with a `slug`, `label`, and `type`.
3. For **single** sections: create `sections/{slug}.md`.
4. For **tabbed** sections: add a `tabs` array (each `{ "id", "label" }`), then create `sections/{slug}/`
   with `_intro.md` and one `{id}.md` file per tab. Every declared tab id must have a matching file.

### Writing guidelines

- Use standard [GitHub Flavored Markdown](https://github.github.com/gfm/).
- Use fenced code blocks with language identifiers (e.g., ` ```php `, ` ```bash `, ` ```ruby `).
- Use `>` blockquotes for callout notes (rendered as styled callout boxes on the site).
- Use Markdown tables for tabular data.
- Keep headings hierarchical: `# Section Title` in `_intro.md`, `## Sub-heading` in content files.

### Local preview

The Markdown is rendered server-side by Laravel's `Str::markdown()` (which uses [league/commonmark](https://commonmark.thephpleague.com/)). Syntax highlighting is applied client-side via [Shiki](https://shiki.style/). Any standard GFM Markdown will render correctly.

## Note

The `README.md` file is not pulled by the site — only `docs.json` and files in `sections/` are fetched.

## Related Repositories

- **[Escalated](https://github.com/escalated-dev/escalated)** — Shared frontend (Vue 3 + Inertia.js)
- **[Escalated for Laravel](https://github.com/escalated-dev/escalated-laravel)** — Laravel Composer package
- **[Escalated for Rails](https://github.com/escalated-dev/escalated-rails)** — Ruby on Rails engine
- **[Escalated for Django](https://github.com/escalated-dev/escalated-django)** — Django reusable app
- **[Escalated for AdonisJS](https://github.com/escalated-dev/escalated-adonis)** — AdonisJS v6 package
- **[Escalated for Filament](https://github.com/escalated-dev/escalated-filament)** — Filament v3 admin panel plugin
- **[Escalated for WordPress](https://github.com/escalated-dev/escalated-wordpress)** — WordPress plugin
- **[Plugin SDK](https://github.com/escalated-dev/escalated-plugin-sdk)** — TypeScript SDK for building plugins
- **[Plugin Runtime](https://github.com/escalated-dev/escalated-plugin-runtime)** — Runtime host for plugins

## License

MIT
