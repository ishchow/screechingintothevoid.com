## Context

Screeching Into The Void is a Quarto-based blog deployed to CloudFlare Pages via GitHub Actions. The site currently uses the default listing style with categories enabled, has no social sharing metadata, uses a placeholder author name in the post scaffolding script, and lacks Copilot instructions. The site targets an austere, literary aesthetic — a table-of-contents style rather than a traditional blog feed.

## Goals / Non-Goals

**Goals:**
- Make the homepage feel like a minimalist table of contents, not a blog feed
- Ensure shared links render rich previews on Slack, Discord, LinkedIn, and Twitter/X
- Streamline the post creation workflow with a Copilot prompt that handles branching
- Orient Copilot to the project architecture via instructions file

**Non-Goals:**
- Redesigning the site theme, typography, or color scheme
- Adding analytics, cookie consent, or any tracking
- Creating custom listing templates
- Changing the deployment pipeline or CI workflow

## Decisions

### 1. Table listing over default or grid

**Decision**: Use `type: table` with `fields: [date, title, reading-time]`.

**Rationale**: The default listing is visually heavy (large cards with images, descriptions, author). Grid is even more visual. A table with three columns feels like a book's table of contents — date, title, reading time — which matches the austere literary vibe. Description is deliberately excluded to keep the landing page spare.

**Alternative considered**: Default type with custom `fields` — still renders as cards, not austere enough.

### 2. Disable all interactive UI controls

**Decision**: Set `sort-ui: false`, `filter-ui: false`, `categories: false`.

**Rationale**: With a low publishing cadence and a small number of posts, sorting/filtering controls add visual noise with no practical value. Categories were never meaningfully used. These can be re-enabled later when the archive grows.

### 3. Open Graph and Twitter Card with minimal config

**Decision**: Set both to `true` in `_quarto.yml` with no custom overrides.

**Rationale**: Quarto auto-generates metadata from page `title`, `description`, and `image` fields. Since posts already have titles and descriptions, this works out of the box. No Twitter handle to configure. Custom overrides add complexity without benefit.

### 4. Footer layout with structured sections

**Decision**: Use Quarto's structured `page-footer` with `center` for copyright and `right` for a GitHub icon link.

**Rationale**: Quarto supports `left`, `center`, `right` footer sections with nav-item syntax. A GitHub icon in the right corner is discoverable but not prominent — fits the minimalist aesthetic. Copyright uses the author's real name since anonymity is not a goal.

### 5. Copilot prompt for new-post workflow over embedding in instructions

**Decision**: Create `.github/prompts/new-post.prompt.md` that creates a branch from `main` (`{year}-{seq}` format) and runs `mise run new-post`.

**Rationale**: The new-post workflow is invoked on demand, not needed as always-on context. A prompt is the right abstraction — triggered when needed, includes specific steps (checkout main, create branch, run mise, open file). The branch naming convention (`2026-002`) keeps things tidy.

### 6. Update scaffolding script defaults

**Decision**: Remove `author` and `categories` from the template, add `description: ""`.

**Rationale**: Author is now inherited from `posts/_metadata.yml`, so specifying it per-post is redundant. Categories are being removed site-wide. The `description` field is added as an empty string to encourage filling it in (needed for Open Graph previews).

### 7. Suppress visible homepage title

**Decision**: Replace `title` with `pagetitle` in `index.qmd`.

**Rationale**: The site title already appears in the navbar. Rendering it again as a page heading is redundant and adds visual noise. Using `pagetitle` preserves the browser tab title without rendering a visible heading.

### 8. Centralize author in shared metadata

**Decision**: Add `author: "Ishaat Chowdhury"` to `posts/_metadata.yml` and remove per-post `author` fields.

**Rationale**: As the sole author, repeating the name in every post is unnecessary. Quarto's `_metadata.yml` inheritance means all posts under `posts/` automatically get the author field. Individual posts can still override if needed (e.g., guest posts).

## Risks / Trade-offs

- **[No description on homepage]** → Visitors must click through to learn what a post is about. Mitigated by descriptive titles and the expectation that this is a personal blog with a small audience.
- **[No sort/filter controls]** → If the post count grows significantly, scanning becomes harder. Mitigated by date-descending sort and the ability to re-enable controls later.
- **[No Twitter handle in twitter-card config]** → Twitter cards will lack `creator` attribution. Low impact since the author doesn't use Twitter.
