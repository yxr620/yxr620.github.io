# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal academic/blog website for Xiangrui Yang, a PhD student at HKU. It uses [Hugo](https://gohugo.io/) with the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme. Pushes to `main` are built and deployed to GitHub Pages by `.github/workflows/hugo.yaml`.

## Commands

```bash
# Start local dev server with live reload
hugo server -D

# Build the site locally (output goes to ignored ./public)
hugo

# Create a new blog post
hugo new blog/<post-name>/index.md
```

Generated files are deployment artifacts and must not be committed. GitHub Actions publishes them directly to <https://yxr620.github.io>.

## Architecture

### Content Structure

- `content/_index.md` — Homepage / CV page (rendered via the custom `layouts/index.html` template)
- `content/blog/` — Blog posts, each in its own subdirectory with `index.md` and optional `pic/` assets
- Blog posts use front matter: `weight`, `title`, `author`, `tags`, `categories`, `date`

### Custom Layouts & Theme Overrides

Hugo uses `layouts/` to override the PaperMod theme. Current overrides:

- `layouts/index.html` — Custom CV-style homepage using `.cv-page` / `.cv-content` CSS classes
- `layouts/partials/extend_head.html` — Injects `static/css/custom.css` and MathJax (for LaTeX rendering)
- `layouts/partials/foot.html` — Additional MathJax CDN script in footer
- `layouts/partials/mathjax.html` — MathJax config partial (also included via archetype)

### Static Assets

- `static/css/custom.css` — All custom styles for the CV page layout; uses PaperMod CSS variables (`--primary`, `--secondary`, `--border`, `--content`) for light/dark mode compatibility
- `static/images/user.jpg` — Profile photo used in the homepage

### MathJax

LaTeX math is supported site-wide. Inline math uses `$...$` or `\(...\)`, display math uses `$$...$$` or `\[\[...\]\]`. The archetype at `archetypes/default.md` includes the MathJax partial automatically for new posts.

### Theme

The active theme is `hugo-PaperMod` located in `themes/hugo-PaperMod/`. Do not edit theme files directly — use `layouts/` overrides instead.
