# Overview

Source code for [screechingintothevoid.com](https://screechingintothevoid.com/).
Built with [soupault](https://soupault.net/).
Hosted on Cloudflare Pages.
Deployed using GitHub Actions.

# Setup

Install [mise](https://mise.jdx.dev/). Then run the following to setup dependencies.

```bash
mise install
```

# Dev Server

```bash
mise serve
```

# Build

```bash
mise build
```

Output is in `build/`.

# Adding New Posts

`mise run new-post "Title"`

# CI/CD

See `.github/workflows/publish.yml` for the CI/CD configuration.
