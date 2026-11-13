# Repository structure

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

## Note

The `README.md` file is not pulled by the site — only `docs.json` and files in `sections/` are fetched.
