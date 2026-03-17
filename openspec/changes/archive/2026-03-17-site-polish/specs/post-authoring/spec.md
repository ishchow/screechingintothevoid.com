## ADDED Requirements

### Requirement: Scaffolding script omits author
The `scripts/new-post.sh` template SHALL NOT include an `author` field in the generated front matter, since author is inherited from `posts/_metadata.yml`.

#### Scenario: No author in scaffolded post
- **WHEN** a new post is scaffolded
- **THEN** the generated `index.qmd` front matter does not contain an `author` line

### Requirement: Scaffolding script omits categories
The `scripts/new-post.sh` template SHALL NOT include a `categories` field in the generated front matter.

#### Scenario: No categories in scaffolded post
- **WHEN** a new post is scaffolded
- **THEN** the generated `index.qmd` front matter does not contain a `categories` line

### Requirement: Scaffolding script includes empty description
The `scripts/new-post.sh` template SHALL include a `description: ""` field to prompt the author to fill it in.

#### Scenario: Description placeholder
- **WHEN** a new post is scaffolded
- **THEN** the generated `index.qmd` front matter contains `description: ""`

### Requirement: Author centralized in shared metadata
The `posts/_metadata.yml` file SHALL include `author: "Ishaat Chowdhury"` so all posts inherit the author automatically.

#### Scenario: Author inherited by posts
- **WHEN** a post does not specify an `author` in its front matter
- **THEN** the rendered post displays "Ishaat Chowdhury" as the author

### Requirement: Hello world post categories and author removed
The `posts/2026/001-hello-world/index.qmd` front matter SHALL have the `categories` and `author` fields removed.

#### Scenario: Existing post updated
- **WHEN** the site is rendered after this change
- **THEN** the hello world post has no `categories` or `author` in its front matter and inherits author from `_metadata.yml`

### Requirement: Copilot prompt for new post workflow
A prompt file SHALL exist at `.github/prompts/new-post.prompt.md` that instructs the agent to create a new post.

#### Scenario: Prompt creates branch from main
- **WHEN** the new-post prompt is invoked
- **THEN** the agent checks out `main`, pulls latest, and creates a new branch named `{year}-{seq}` (e.g., `2026-002`)

#### Scenario: Prompt runs mise scaffolding
- **WHEN** the new-post prompt is invoked with a title
- **THEN** the agent runs `mise run new-post "<title>"` to scaffold the post directory

#### Scenario: Prompt opens the new file
- **WHEN** the scaffolding completes
- **THEN** the agent opens the newly created `index.qmd` for editing
