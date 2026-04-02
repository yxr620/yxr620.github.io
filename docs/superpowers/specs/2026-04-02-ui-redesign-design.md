# UI Redesign — Graphite Lab Design Spec

**Date:** 2026-04-02
**Approach:** C — Hybrid (CSS-driven everywhere possible; new layout overrides only where HTML structure is required)

---

## Goals

1. Unify blog list and article pages with the same visual language as the homepage.
2. Compress homepage copy; fold secondary sections; keep all content accessible.
3. Shift to a colder, darker palette with a terminal / research-lab aesthetic.

---

## 1. Color System & Global Styles

### Dark mode tokens (added to `.dark` in `custom.css`)

Two layers must be updated: the custom `--cv-*` tokens, and PaperMod's base tokens (which control `background`, `color`, `border` site-wide).

**PaperMod base token overrides (`.dark` block):**

| Token | New value | Notes |
|---|---|---|
| `--theme` | `#111318` | Page background |
| `--entry` | `#16191f` | Card / panel backgrounds |
| `--primary` | `#dde2ec` | Primary text / headings |
| `--secondary` | `rgba(160,180,255,0.55)` | Secondary / meta text |
| `--content` | `#a8b0c0` | Body prose |
| `--border` | `rgba(160,180,255,0.10)` | Dividers |

**Custom `--cv-*` token overrides (`.dark` block):**

| Token | Value | Usage |
|---|---|---|
| `--cv-accent` | `#00e5c0` | Links, active states, decorative glyphs |
| `--cv-accent-soft` | `rgba(0,229,192,0.12)` | Soft accent backgrounds |
| `--cv-panel` | `rgba(255,255,255,0.03)` | Subtle panel fill |
| `--cv-heading` | `#dde2ec` | h1–h3 (mirrors `--primary`) |
| `--cv-dim` | `rgba(160,180,255,0.35)` | Meta, labels, dates |

Light mode palette is **unchanged** — no regression.

### Global

- Monospace font stack unchanged: SF Mono / JetBrains Mono / IBM Plex Mono.
- Sans-serif stack unchanged: Avenir Next / IBM Plex Sans / Segoe UI.
- Grid backdrop pattern (currently homepage-only) extended to blog list and article pages via a shared `.page-grid-bg` pseudo-element class. Same `opacity: 0.28`, same `mask-image` fade.

---

## 2. Homepage — Typographic Drama

**Files changed:** `static/css/custom.css`, `content/_index.md`
**Files unchanged:** `layouts/index.html` (no structural change needed)

### 2a. Header block

- `.cv-header h1` renders name in two stacked lines: `Xiangrui` / `Yang`.
- Font size: `clamp(3.5rem, 12vw, 5.5rem)`, weight 700, letter-spacing `-0.06em`, line-height `0.88`.
- Gradient fill: `background: linear-gradient(90deg, #dde2ec, #6a80b0)` with `background-clip: text; -webkit-text-fill-color: transparent`.
- "XY" watermark: absolute-positioned `::before` pseudo on `.cv-header`, content `"XY"`, font-size `8rem`, monospace, `color: rgba(0,229,192,0.04)`, `z-index: 0`, pointer-events none.
- Tag pill (`.cv-subtitle`): border updates to `rgba(0,229,192,0.25)`, text color `var(--cv-accent)`.

### 2b. Hero card bio — two-level expand

Short bio (always visible):
> PhD @ HKU, advised by Yiming Qiu. MSc @ HUST · BSc @ SYSU. Research: ML systems, storage, HPC.

Full bio (inside `<details>` in `_index.md`, expanded on click):
> PhD student @ HKU, advised by Prof. Yiming Qiu. MSc CS @ HUST (adv. Prof. Qiang Cao) · BSc CS @ SYSU (adv. Prof. Yuedong Yang).
>
> Research: optimizing ML systems and HPC — CUDA, DGL, sparse matrix acceleration. Explored sparse ops in ad-ranking systems at Tencent.
>
> Outside academia: economics and investment.

`<details>` lives inside `.cv-hero-text`, replacing the current `<p class="cv-hero-bio">`. CSS:
- `summary`: display block, cursor pointer, color `var(--cv-body)`; `::marker` hidden; custom `▸`/`▾` glyph in `var(--cv-accent)` via `::before`.
- Expanded content: `padding-top: 0.6rem`, same body styles as short bio.

### 2c. Section accordion folds

Sections wrapped in `<details>`/`<summary>` in `content/_index.md`:
- **Folded** (closed by default): Education Background, Talks & Presentations, Internship, Academic Projects, Certificates and Awards.
- **Open** (no fold): Academic Papers — rendered as a normal `h2`, stays fully visible.

CSS for `details` inside `.cv-content`:
- `summary` styled identically to `.cv-content h2`: counter increment, border-bottom, monospace `01` prefix, `font-size: 1.4rem`, weight 650.
- `summary::marker`: `display: none`.
- `summary::before`: content `"▸ "` (closed) / `"▾ "` (open via `details[open] summary::before`), color `var(--cv-accent)`, monospace.
- `details[open]`: no extra padding — content flows naturally.
- No JS animation needed; native `<details>` toggle is sufficient.

---

## 3. Blog List — Compact List

**File created:** `layouts/_default/list.html` (overrides PaperMod default)

### Page header

Same visual as homepage `h2` sections: monospace `01` counter prefix, border-bottom, `"Blog"` title.

### Entry structure (per post)

```html
<article class="post-entry">
  <a class="post-entry-link" href="{{ .Permalink }}">
    <div class="post-entry-meta">{{ .Date.Format "2006-01-02" }}</div>
    <h2 class="post-entry-title">{{ .Title }}</h2>
    {{ with .Params.categories }}
    <div class="post-entry-tags">
      {{ range . }}{{ . }} · {{ end }}
    </div>
    {{ end }}
    <p class="post-entry-summary">{{ .Summary | plainify | truncate 120 }}</p>
  </a>
</article>
```

> **Note:** existing posts use `categories` in front matter (e.g. `categories: ["blog"]`), not `tags`. The template uses `.Params.categories`. If posts later add `tags`, the template can be extended to show both.

### CSS (in `custom.css`)

| Element | Style |
|---|---|
| `.post-entry` | `padding: 1rem 0`, `border-bottom: 1px solid var(--cv-border)`, no card shadow |
| `.post-entry-meta` | monospace, `0.72rem`, `var(--cv-dim)`, `letter-spacing: 0.08em` |
| `.post-entry-title` | `var(--cv-heading)`, `1rem`, weight 600, `letter-spacing: -0.02em` |
| `.post-entry-tags` | monospace, `var(--cv-accent)`, `0.68rem`, `·` separated |
| `.post-entry-summary` | `var(--cv-body)`, `0.85rem`, max `60ch`, single line, `text-overflow: ellipsis` |
| `.post-entry:hover .post-entry-title` | `color: var(--cv-accent)`, transition `0.15s` |
| `.post-entry-link` | `text-decoration: none`, `display: block` |

Grid backdrop applied via a `.list-page` wrapper `<div>` that `list.html` emits around all entries. The `::after` pseudo-element on `.list-page` carries the grid pattern (same as `.cv-page::after`).

The `list.html` template must extend `baseof.html` via `{{- define "main" }}` and must include the `{{ partial "extend_head.html" . }}` is already injected globally — no extra action needed. MathJax is also already global.

---

## 4. Article Page — Lab Notebook

**File created:** `layouts/_default/single.html` (overrides PaperMod default)

### Layout

Two-column CSS grid: `grid-template-columns: 200px 1fr`, `gap: 2.5rem`, wrapped in `.lab-page`.

### HTML structure

```html
<div class="lab-page">
  <aside class="lab-sidebar">
    <div class="lab-breadcrumb">
      <a href="/blog/">~/blog</a> /
    </div>
    <nav class="lab-toc">
      {{ .TableOfContents }}
    </nav>
    <div class="lab-meta">
      <div class="lab-date">{{ .Date.Format "2006-01-02" }}</div>
      {{ with .Params.tags }}
      <div class="lab-tags">
        {{ range . }}<span class="lab-tag">{{ . }}</span>{{ end }}
      </div>
      {{ end }}
    </div>
  </aside>
  <article class="lab-content post-content">
    <header class="lab-header">
      <h1>{{ .Title }}</h1>
    </header>
    {{ .Content }}
  </article>
</div>
```

### CSS (in `custom.css`)

**Sidebar:**
| Property | Value |
|---|---|
| `position` | `sticky` |
| `top` | `5rem` |
| `height` | `fit-content` |
| `max-height` | `calc(100vh - 6rem)` |
| `overflow-y` | `auto` |
| Font | monospace, `0.72rem`, `var(--cv-dim)`, line-height `2` |

**TOC links:**
- Default: `var(--cv-dim)`, no underline.
- Active (`.active`): `color: var(--cv-accent)`, `border-left: 2px solid var(--cv-accent)`, `padding-left: 0.5rem`.

**Scroll-spy:** small inline `<script>` in `single.html` using `IntersectionObserver` on all `h2`/`h3` elements. On intersection, adds `.active` class to the matching TOC `<a>`. No dependencies.

**Article header:**
- `h1`: gradient fill matching homepage name (`#dde2ec → #6a80b0`), `clamp(2rem, 6vw, 3rem)`, weight 700.
- `h2`/`h3`: same accent-bar style as `.cv-content h2`/`h3`.

**Mobile (`max-width: 768px`):**
- Sidebar hidden (`display: none`).
- Date and tags shown inline above `h1` in `.lab-header`.
- Grid collapses to single column.

---

## Files Changed Summary

| File | Action |
|---|---|
| `static/css/custom.css` | Update dark tokens; add homepage drama styles; blog list styles; article sidebar styles; `details`/`summary` accordion styles |
| `content/_index.md` | Compress bio; wrap sections in `<details>`; add expandable full-bio `<details>` in hero |
| `layouts/_default/list.html` | New file — Compact List override |
| `layouts/_default/single.html` | New file — Lab Notebook override with scroll-spy script |

**Not touched:** `layouts/index.html`, theme files, `config.yml`, any other content.
