# Contributing

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
