## Context

This is a greenfield project — no existing code, infrastructure, or content. The repository currently contains only the `openspec/` directory. The target is a personal blog for long-form written content (book reviews, essays) with academic-style numbered citations.

The architecture is: **Quarto (static site generator) → GitHub Actions (CI/CD) → CloudFlare Pages (hosting)**.

Key constraints from exploration:
- Quarto URLs are filesystem-path-based; there is no Hugo-like permalink config
- CloudFlare Pages is not officially listed in Quarto's publishing docs but works via `cloudflare/pages-action`
- The blog has no executable code (R/Python/Julia) — pure markdown-to-HTML rendering
- The author publishes a few times per year, so the directory structure should balance organization without excessive nesting

## Goals / Non-Goals

**Goals:**
- Fully functional Quarto blog with flatly/darkly theme toggle
- Top navbar with title (left), About + search + theme toggle (right)
- IEEE `[1]` numbered citation style with per-post `.bib` files
- Directory structure: `posts/{year}/{NNN}-{slug}/index.qmd` (3-digit zero-padded sequence)
- Automated deploy to CloudFlare Pages on push to `main`
- PR preview deploys for draft review
- `mise run new-post` task to scaffold posts with correct structure and boilerplate
- RSS feed for the blog

**Non-Goals:**
- Custom domain DNS setup (user already has this on CloudFlare)
- Blog content authoring (user will write their own content)
- Comments system, analytics, or newsletter integration
- Executable code cells (R/Python/Julia) in blog posts
- Custom Quarto extensions or shortcodes
- Search engine optimization beyond basic metadata

## Decisions

### 1. Deployment: GitHub Actions + `cloudflare/pages-action` over CF Pages direct build

**Choice**: Render in GitHub Actions, deploy pre-built `_site/` to CF Pages.

**Rationale**: CF Pages build environment doesn't include Quarto natively. While a custom build command can install it, this is fragile and harder to debug. GitHub Actions with `quarto-dev/quarto-actions/setup@v2` is the well-supported path. It also enables pinning Quarto versions and better build failure diagnostics.

**Alternative considered**: CF Pages direct build with inline Quarto install — rejected due to fragility and lack of version pinning.

### 2. Theme: Flatly (light) / Darkly (dark) paired toggle

**Choice**: Use Quarto's built-in light/dark theme switching with the flatly/darkly Bootswatch pair.

**Rationale**: Flatly and darkly are designed as a matched light/dark pair with consistent fonts and spacing. Quarto automatically adds a theme toggle icon to the navbar when both are specified.

### 3. Citation style: IEEE via CSL file in project root

**Choice**: Download `ieee.csl` to the project root, reference it from `posts/_metadata.yml` so all posts inherit it.

**Rationale**: IEEE's `[1]` numbered style is the best fit for a blog context per the user's preference. Per-post `.bib` files keep references self-contained. The CSL file in the root with a relative path from `_metadata.yml` (`csl: ../ieee.csl`) ensures consistency without per-post repetition.

### 4. Directory structure: `posts/{year}/{NNN}-{slug}/`

**Choice**: Two-level nesting — year folder containing zero-padded 3-digit sequence + slug folders.

**Rationale**: Provides filesystem ordering within a year without excessive nesting. The user publishes a few times per year, so year-level grouping is sufficient. 3-digit padding (001-999) allows up to 999 posts per year. The listing page uses `contents: "posts/**/index.qmd"` recursive glob.

**Alternative considered**: Full date nesting (`YYYY/MM/DD/slug`) — rejected as too deep for the publishing frequency. Flat structure — rejected as not providing enough organization.

### 5. Post scaffolding: mise task wrapping a shell script

**Choice**: `mise run new-post "Title"` backed by a bash script.

**Rationale**: The user already uses mise. A mise task is discoverable via `mise tasks`, needs no additional runtime (pure bash), and the `mise.toml` can exist with only `[tasks]` — no `[tools]` section needed. The script auto-detects the year and next sequence number.

## Risks / Trade-offs

- **[Quarto URL rigidity]** → URLs are locked to filesystem paths. Changing the directory scheme later would break all existing links. Mitigated by choosing a structure the user is comfortable with upfront.
- **[CloudFlare Pages deprecation signals]** → CF has hinted at migrating Pages toward Workers for static sites. Mitigated by the fact that the GH Actions workflow only calls `pages-action` in one step — easy to swap to `wrangler` Workers deploy if needed.
- **[IEEE CSL file maintenance]** → The CSL file is vendored into the repo. If the IEEE style is updated, it must be manually refreshed. Low risk given citation style stability.
- **[No local Quarto requirement enforced]** → The mise task only needs bash, but local preview requires Quarto installed. This is intentional — the user can install Quarto independently.
