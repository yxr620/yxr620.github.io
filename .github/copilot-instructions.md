# Project Guidelines

## Overview

Hugo static site for Xiangrui Yang's academic blog/CV. Theme: **PaperMod** (`themes/hugo-PaperMod/`). Pushes to `main` are built and deployed to `https://yxr620.github.io` by `.github/workflows/hugo.yaml`.

## Commands

```bash
hugo server -D        # Dev server with drafts
hugo                  # Local build → ignored ./public
hugo new blog/<name>/index.md  # New blog post
```

## Architecture

- `content/_index.md` — CV/resume homepage (custom layout, not blog index)
- `content/blog/<slug>/index.md` — Blog posts, each in own directory; images go in `pic/` subfolder
- `layouts/` — Theme overrides (never edit files in `themes/` directly)
- `layouts/index.html` — Custom CV homepage using `.cv-page` / `.cv-content` classes
- `static/css/custom.css` — All custom styles; uses PaperMod CSS variables (`--primary`, `--secondary`, `--border`, `--content`) for light/dark mode

## Conventions

### Blog Post Front Matter

All posts use YAML front matter with these fields:

```yaml
title: "标题"
author: "yxr620"
tags: ["tag1"]
categories: ["blog"]
toc:
  enable: true
  auto: true
date: 2024-01-01T00:00:00+08:00
draft: false
weight: 3
```

- Content is written in **Chinese (Simplified)**
- Topics are finance/economics focused with heavy LaTeX math

### MathJax

LaTeX is supported site-wide. Use `$...$` for inline math, `$$...$$` for display math. The archetype auto-includes the MathJax partial for new posts.

### Styling

- Use PaperMod CSS variables for theme compatibility — don't hardcode colors
- Dark mode: use `.dark` selector when needed
- Responsive breakpoint at `768px`

### Key Rules

- **Never edit theme files** — override via `layouts/` or `static/`
- `profileMode` is disabled in config; the custom `layouts/index.html` renders the CV homepage instead
- Goldmark `unsafe: true` is enabled — raw HTML in markdown is allowed
