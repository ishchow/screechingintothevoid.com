# Copilot Instructions

## Project Overview

This is a static site built with [soupault](https://soupault.app/) (v5.3.0). Pages are authored in HTML or Markdown and assembled using a template (`templates/main.html`). Configuration lives in `soupault.toml`.

## Build

- Build tool: [mise](https://mise.jdx.dev/)
- Build command: `mise run build`
- Output directory: `build/`

## Lua Plugins / Index Views

Soupault's plugin/index scripting environment uses **Lua 2.5** (via Lua-ML). This means:

- The `string` library (e.g. `string.sub`, `string.find`) does **not** exist.
- Use global functions instead: `strsub`, `strfind`, `strlen`, `strupper`, `strlower`, `format`, etc.
- Table iteration uses `while` loops with numeric indices (no `pairs`/`ipairs`).
- Soupault provides its own APIs: `HTML.*`, `Regex.*`, `Table.*`, `JSON.*`, `Sys.*`, etc.

## Directory Structure

- `site/` — source pages and assets
- `site/posts/` — blog posts organized by year
- `templates/` — page templates
- `build/` — generated output (git-ignored)
- `scripts/` — helper scripts (e.g. `new-post.sh`)
