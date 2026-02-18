# Escalated Documentation

This repository contains the documentation for [Escalated](https://escalated.dev), an open-source embeddable support ticket system.

The Markdown files in this repo are fetched at runtime by the Escalated marketing site and rendered as the [/docs](https://escalated.dev/docs) page.

## Structure

```
docs.json              # Manifest — defines section order, sidebar labels, and types
sections/
  getting-started.md   # Framework-agnostic sections are single files
  installation/        # Framework-specific sections are directories
    _intro.md          # Shared intro text (appears above the tab switcher)
    laravel.md         # Per-framework content
    rails.md
    django.md
    adonis.md
    filament.md
    wordpress.md
  ...
```

### Section types

- **`single`** — A standalone Markdown file for content that applies to all frameworks.
- **`tabbed`** — A directory containing `_intro.md` (shared heading + intro paragraph) and one Markdown file per framework. The site renders these with a framework tab switcher.

## Contributing

### Editing existing docs

1. Find the section you want to edit in the `sections/` directory.
2. Edit the Markdown file directly on GitHub or clone the repo locally.
3. Open a pull request with your changes.

Changes merged to `main` will appear on the site within one hour (the cache TTL), or immediately if the cache is cleared.

### Adding a new section

1. Add a new entry to `docs.json` with the section's `slug`, `label`, `anchor`, and `type`.
2. Create the corresponding Markdown file(s) in `sections/`.
3. For **single** sections: create `sections/{slug}.md`.
4. For **tabbed** sections: create `sections/{slug}/` with `_intro.md` and a file for each framework.

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
