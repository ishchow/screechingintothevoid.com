## ADDED Requirements

### Requirement: Copilot instructions file exists
A file SHALL exist at `.github/copilot-instructions.md` providing project context to Copilot.

#### Scenario: File present in repository
- **WHEN** Copilot is invoked in this repository
- **THEN** it loads `.github/copilot-instructions.md` as context

### Requirement: Instructions describe site architecture
The instructions file SHALL document the technology stack (Quarto, GitHub Actions, CloudFlare Pages), the directory structure for posts (`posts/{year}/{NNN}-{slug}/`), and the deployment pipeline.

#### Scenario: Architecture overview present
- **WHEN** reading the instructions file
- **THEN** it contains sections covering the tech stack, directory layout, and deployment flow

### Requirement: Instructions describe post creation workflow
The instructions file SHALL document how to create a new post using `mise run new-post "<title>"` and the branch naming convention (`{year}-{seq}`).

#### Scenario: Post workflow documented
- **WHEN** reading the instructions file
- **THEN** it contains the mise command for creating posts and explains the branch naming convention

### Requirement: Instructions describe key conventions
The instructions file SHALL document key conventions: IEEE citation style with per-post `refs.bib` files, posts created as drafts by default, and the `posts/_metadata.yml` shared configuration.

#### Scenario: Conventions documented
- **WHEN** reading the instructions file
- **THEN** it contains information about the citation system, draft workflow, and shared metadata
