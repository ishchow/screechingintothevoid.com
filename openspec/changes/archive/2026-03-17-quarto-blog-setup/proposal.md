## Why

This is a greenfield blog project for screechingintothevoid.com. The site needs to support long-form written content (book reviews, essays) with academic-style citations. Quarto is the authoring tool of choice for its native BibTeX/citation support and markdown-first workflow. The site will be deployed to CloudFlare Pages for its AI bot blocking, analytics, and CDN capabilities.

## What Changes

- Scaffold a complete Quarto blog project with flatly/darkly theme toggle
- Configure top navbar navigation (title left, About + search + theme toggle right)
- Set up IEEE citation style (`[1]` numbered references) with per-post `.bib` files
- Establish a date-organized post directory structure: `posts/{year}/{seq}-{slug}/`
- Create a GitHub Actions CI/CD pipeline that renders the site and deploys to CloudFlare Pages via `cloudflare/pages-action`
- Enable PR preview deploys for draft review
- Add a `mise run new-post` task to scaffold new blog posts with boilerplate

## Capabilities

### New Capabilities
- `blog-scaffold`: Quarto blog project structure, theme configuration, navbar, listing page, and about page
- `citation-system`: IEEE citation style with per-post bibliography files and shared CSL configuration
- `deployment-pipeline`: GitHub Actions workflow for rendering Quarto and deploying to CloudFlare Pages with PR previews
- `post-authoring`: mise task for scaffolding new posts with correct directory structure, front matter template, and empty `.bib` file

### Modified Capabilities
<!-- No existing capabilities to modify — this is a greenfield project. -->

## Impact

- **New files**: Full Quarto project scaffold (`_quarto.yml`, `index.qmd`, `about.qmd`, `styles.css`, `ieee.csl`, `posts/_metadata.yml`), GitHub Actions workflow, mise configuration
- **Dependencies**: Quarto (build-time via GH Actions), CloudFlare Pages (hosting), mise (local dev tooling)
- **External services**: Requires CloudFlare API token and account ID as GitHub secrets; requires a CloudFlare Pages project to be created
- **Domain**: Existing CloudFlare-managed domain will be pointed to the Pages project
