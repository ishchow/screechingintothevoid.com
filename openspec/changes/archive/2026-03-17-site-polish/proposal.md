## Why

The blog's homepage uses Quarto's default listing style, which is visually heavy for a site aiming for an austere, literary aesthetic. Categories add unnecessary clutter with only one post. Social metadata (Open Graph, Twitter Cards) is missing, so shared links appear as plain URLs. The post scaffolding script has stale defaults (placeholder author, empty categories array), and there's no Copilot instructions file to orient the AI agent to the project's architecture.

## What Changes

- Remove the visible title from the homepage (use `pagetitle` instead of `title` so the browser tab is set but no heading renders)
- Switch the homepage listing from `default` type to `table` with only `date`, `title`, and `reading-time` fields
- Disable categories site-wide and remove them from the hello world post
- Disable sort and filter UI controls for a cleaner landing page
- Enable `table-hover` for row interactivity
- Add Open Graph and Twitter Card metadata generation (`true` for both)
- Update the page footer: copyright under "Ishaat Chowdhury" with a GitHub icon linking to the source repository
- Move `author` to `posts/_metadata.yml` so all posts inherit it; remove per-post `author` fields
- Update `scripts/new-post.sh`: remove `categories` and `author` from the template
- Create `.github/prompts/new-post.prompt.md` that runs the mise scaffolding command and creates a new branch from `main` named `{year}-{seq}` (e.g., `2026-002`)
- Create `.github/copilot-instructions.md` documenting the site architecture and conventions

## Capabilities

### New Capabilities
- `homepage-listing`: Table-style listing configuration with minimal fields, no categories, no sort/filter UI, and hover styling
- `site-metadata`: Open Graph and Twitter Card metadata generation, updated footer with real-name copyright and source code link
- `post-authoring`: Updated scaffolding script defaults and a Copilot prompt for the new-post workflow including branch creation
- `copilot-instructions`: Repository-level Copilot instructions documenting site architecture and conventions

### Modified Capabilities

## Impact

- `index.qmd`: Listing configuration rewrite, replace `title` with `pagetitle`
- `_quarto.yml`: New `open-graph`, `twitter-card`, and updated `page-footer` configuration
- `posts/_metadata.yml`: Add `author: "Ishaat Chowdhury"`
- `posts/2026/001-hello-world/index.qmd`: Remove `categories` and `author` front matter fields
- `scripts/new-post.sh`: Updated template defaults (no author, no categories, add description)
- `.github/prompts/new-post.prompt.md`: New file
- `.github/copilot-instructions.md`: New file
