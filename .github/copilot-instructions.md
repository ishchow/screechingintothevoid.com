# Screeching Into The Void

A personal blog for long-form essays and book reviews, built for an austere literary aesthetic.

## Tech Stack

- **Quarto** — Static site generator (`.qmd` files → HTML)
- **GitHub Actions** — CI/CD (`.github/workflows/publish.yml`)
- **CloudFlare Pages** — Hosting and CDN

## Directory Structure

```
posts/
├── _metadata.yml          # Shared metadata (author, citation style, freeze)
└── {year}/
    └── {NNN}-{slug}/
        ├── index.qmd      # Post content
        └── refs.bib        # Per-post BibTeX references
```

- `{year}` — Four-digit year (e.g., `2026`)
- `{NNN}` — Three-digit zero-padded sequence number (e.g., `001`)
- `{slug}` — Slugified title (e.g., `hello-world`)
- URLs follow the filesystem path: `/posts/2026/001-hello-world/`

## Deployment Pipeline

1. Push to `main` or open a PR triggers `.github/workflows/publish.yml`
2. GitHub Actions installs Quarto, renders the site, deploys `_site/` to CloudFlare Pages
3. PRs get preview deploys; pushes to `main` deploy to production

## Creating a New Post

Use the mise task runner:

```bash
mise run new-post "My Post Title"
```

This scaffolds `posts/{year}/{NNN}-{slug}/index.qmd` and an empty `refs.bib`. Posts are created as **drafts by default** — set `draft: false` in the front matter when ready to publish.

### Branch Naming Convention

New post branches are named `{year}-{NNN}` (e.g., `2026-002`), always created from `main`.

## Key Conventions

- **Author**: Set globally in `posts/_metadata.yml`. Do not add `author` to individual post front matter unless overriding.
- **Citations**: IEEE numbered style (`[1]`) via `ieee.csl` at the project root, configured in `posts/_metadata.yml`. Each post has its own `refs.bib` file.
- **No categories**: The site does not use categories.
- **Homepage listing**: Table format showing date, title, and reading time only.
- **Description field**: Every post should have a `description` in its front matter — this powers Open Graph and RSS previews.
- **Freeze**: Enabled in `posts/_metadata.yml`. Quarto caches rendered output to avoid re-executing computational content.
