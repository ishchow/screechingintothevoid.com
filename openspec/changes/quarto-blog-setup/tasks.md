## 1. Quarto Project Scaffold

- [x] 1.1 Create `_quarto.yml` with website project type, `_site` output dir, flatly/darkly theme toggle, top navbar (title left; About, search, theme toggle right), and RSS feed config
- [x] 1.2 Create `index.qmd` as the blog listing page with `contents: "posts/**/index.qmd"`, date descending sort, and categories enabled
- [x] 1.3 Create `about.qmd` with placeholder about page content
- [x] 1.4 Create `styles.css` as an empty custom stylesheet referenced in `_quarto.yml`
- [x] 1.5 Create `posts/_metadata.yml` with shared post defaults: `freeze: true`, `citation: true`, `csl: ../ieee.csl`
- [x] 1.6 Create `.gitignore` with entries for `_site/`, `_freeze/`, `.quarto/`, and other Quarto build artifacts

## 2. Citation System

- [x] 2.1 Download `ieee.csl` from the Citation Style Language repository and place it at the project root
- [x] 2.2 Verify citation config by creating a sample post with a `.bib` entry and confirming IEEE `[1]` style renders correctly (remove sample post after verification)

## 3. Deployment Pipeline

- [x] 3.1 Create `.github/workflows/publish.yml` with GitHub Actions workflow: trigger on push to `main` and `pull_request`, install Quarto via `quarto-dev/quarto-actions/setup@v2`, run `quarto render`, deploy `_site/` via `cloudflare/pages-action@v1` with secrets for `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`, and `GITHUB_TOKEN`
- [x] 3.2 Set workflow permissions to `contents: read` and `deployments: write`

## 4. Post Scaffolding Task

- [x] 4.1 Create `mise.toml` at project root with a `new-post` task definition that accepts a title argument and calls the scaffolding script
- [x] 4.2 Create `scripts/new-post.sh` that: auto-detects current year, finds next 3-digit zero-padded sequence number, slugifies the title (lowercase, hyphens, strip special chars), creates `posts/{year}/{seq}-{slug}/index.qmd` with front matter template (title, author placeholder, today's date, empty categories, `bibliography: refs.bib`, `draft: true`), creates empty `refs.bib`, and prints the created path
- [x] 4.3 Verify the mise task runs correctly end-to-end: `mise run new-post "Test Post"` creates the expected directory structure and files (clean up test output after)

## 5. Verification

- [x] 5.1 Run `quarto render` and confirm the site builds successfully with no errors
- [x] 5.2 Confirm the listing page discovers posts via the recursive glob
- [x] 5.3 Confirm the navbar displays correctly with title, About link, search, and theme toggle
- [ ] 5.4 Commit all files to the repository
