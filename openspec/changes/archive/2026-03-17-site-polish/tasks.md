## 1. Homepage Listing

- [x] 1.1 Update `index.qmd`: replace `title` with `pagetitle: "Screeching Into The Void"`
- [x] 1.2 Update `index.qmd` listing: change `type` to `table`, add `fields: [date, title, reading-time]`, set `categories: false`, `sort-ui: false`, `filter-ui: false`, `table-hover: true`
- [x] 1.3 Remove `categories` and `author` fields from `posts/2026/001-hello-world/index.qmd` front matter

## 2. Site Metadata and Footer

- [x] 2.1 Add `open-graph: true` and `twitter-card: true` under the `website` key in `_quarto.yml`
- [x] 2.2 Update `page-footer` in `_quarto.yml`: set `center` to "© 2026 Ishaat Chowdhury", add `right` section with GitHub icon linking to `https://github.com/ishchow/screechingintothevoid.com`

## 3. Post Scaffolding and Author Metadata

- [x] 3.1 Add `author: "Ishaat Chowdhury"` to `posts/_metadata.yml`
- [x] 3.2 Update `scripts/new-post.sh`: remove `author` and `categories` lines from the template, add `description: ""`

## 4. Copilot Prompt for New Post

- [x] 4.1 Create `.github/prompts/new-post.prompt.md` with instructions to: check out `main`, pull latest, determine year and next sequence number, create branch `{year}-{seq}`, run `mise run new-post "<title>"`, and open the generated file

## 5. Copilot Instructions

- [x] 5.1 Create `.github/copilot-instructions.md` documenting: tech stack (Quarto + GitHub Actions + CloudFlare Pages), directory structure (`posts/{year}/{NNN}-{slug}/`), deployment pipeline, post creation workflow (`mise run new-post`), branch naming convention, citation system (IEEE with per-post `refs.bib`), shared `posts/_metadata.yml` config, and draft-by-default workflow

## 6. Verification

- [x] 6.1 Run `quarto render` and verify the site builds without errors
- [x] 6.2 Verify the homepage renders as a table with the correct columns
