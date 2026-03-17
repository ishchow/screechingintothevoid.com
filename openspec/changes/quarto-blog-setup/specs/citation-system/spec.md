## ADDED Requirements

### Requirement: IEEE citation style
All blog posts SHALL use the IEEE citation style, rendering in-text citations as numbered references (e.g., `[1]`). The IEEE CSL file (`ieee.csl`) SHALL be stored at the project root.

#### Scenario: Numbered citations render correctly
- **WHEN** a post contains `[@AuthorKey2026]` and a corresponding entry exists in the post's `.bib` file
- **THEN** the rendered post displays a numbered citation like `[1]` inline and a formatted reference in the bibliography section

### Requirement: Per-post bibliography files
Each blog post SHALL have its own `refs.bib` file in its post directory, declared via `bibliography: refs.bib` in the post's front matter.

#### Scenario: Post-specific references
- **WHEN** a post at `posts/2026/001-example/index.qmd` has `bibliography: refs.bib` in its front matter
- **THEN** citations in that post resolve against `posts/2026/001-example/refs.bib`

### Requirement: Shared citation configuration
The `posts/_metadata.yml` file SHALL set `csl: ../ieee.csl` so all posts inherit the IEEE citation style without per-post repetition.

#### Scenario: Citation style inheritance
- **WHEN** a new post is created without a `csl:` field in its front matter
- **THEN** the post uses the IEEE citation style inherited from `posts/_metadata.yml`

### Requirement: Bibliography section placement
Each post SHALL render a "References" section at the end containing all cited works.

#### Scenario: References section appears
- **WHEN** a post with citations is rendered
- **THEN** a numbered "References" section appears at the bottom of the post
