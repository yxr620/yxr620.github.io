# UI Redesign — Graphite Lab Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Overhaul the blog's visual identity to a Graphite Lab dark aesthetic, unifying homepage, blog list, and article pages under one visual language.

**Architecture:** Hybrid — CSS-driven for colors/typography/decoration; new Hugo layout overrides only where HTML structure demands it (blog list and article page). Homepage restructured with native `<details>` accordion folds. One small vanilla-JS `IntersectionObserver` for article TOC scroll-spy, no dependencies.

**Tech Stack:** Hugo static site generator, PaperMod theme, plain CSS, vanilla JS.

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `static/css/custom.css` | Modify — append blocks | All new styles: dark tokens, typography drama, accordion CSS, list entries, lab sidebar |
| `content/_index.md` | Modify — full rewrite | Compressed bio with expand; sections wrapped in `<details>` as raw HTML |
| `layouts/_default/list.html` | Create | Compact List blog index template |
| `layouts/_default/single.html` | Create | Lab Notebook article layout with scroll-spy script |

> **Markdown inside `<details>` note:** Hugo's Goldmark renderer treats `<details>` as a raw HTML block and will not process markdown inside it. All content inside `<details>` in `_index.md` is therefore written as HTML, not markdown.

---

## Task 1: Update dark mode color tokens

**Files:**
- Modify: `static/css/custom.css` — `.dark` block (lines 11–17)

- [ ] **Step 1: Replace the `.dark` block**

In `static/css/custom.css`, find and replace the existing `.dark { … }` block (currently lines 11–17) with:

```css
.dark {
    /* PaperMod base token overrides */
    --theme: #111318;
    --entry: #16191f;
    --primary: #dde2ec;
    --secondary: rgba(160, 180, 255, 0.55);
    --content: #a8b0c0;
    --border: rgba(160, 180, 255, 0.10);

    /* cv custom tokens */
    --cv-accent: #00e5c0;
    --cv-accent-soft: rgba(0, 229, 192, 0.12);
    --cv-panel: rgba(255, 255, 255, 0.03);
    --cv-grid: rgba(160, 180, 255, 0.08);
    --cv-shadow: 0 26px 70px rgba(0, 0, 0, 0.4);
}
```

- [ ] **Step 2: Start dev server and verify dark mode colors**

```bash
hugo server -D
```

Open http://localhost:1313, click the theme toggle (sun/moon icon) to enable dark mode. Verify:
- Page background is dark charcoal `#111318`
- Body text is cool grey `#a8b0c0`
- The `/` separators in the nav are now cyan (`#00e5c0`), not blue
- Toggle back to light mode — no visual regression (still the original light palette)

- [ ] **Step 3: Commit**

```bash
git add static/css/custom.css
git commit -m "feat: update dark mode tokens to Graphite Lab palette"
```

---

## Task 2: Homepage header — Typographic Drama

**Files:**
- Modify: `static/css/custom.css` — append to end of file

- [ ] **Step 1: Append Typographic Drama styles**

Append the following block to the very end of `static/css/custom.css`:

```css
/* ============================================================
   TYPOGRAPHIC DRAMA — Homepage header (dark mode only)
   ============================================================ */

.cv-header {
    position: relative;
    overflow: hidden;
}

/* Gradient name fill */
.dark .cv-header h1 {
    font-size: clamp(3.5rem, 12vw, 5.5rem);
    letter-spacing: -0.06em;
    line-height: 0.88;
    background: linear-gradient(100deg, #dde2ec 30%, #6a80b0 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

/* Keep h1 above the watermark */
.cv-header h1 {
    position: relative;
    z-index: 1;
}

/* "XY" faint watermark */
.dark .cv-header::before {
    content: "XY";
    position: absolute;
    right: -0.5rem;
    top: -1rem;
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 9rem;
    font-weight: 700;
    color: rgba(0, 229, 192, 0.035);
    letter-spacing: -0.06em;
    line-height: 1;
    pointer-events: none;
    user-select: none;
    z-index: 0;
}

/* Tag pill — cyan border + text in dark mode */
.dark .cv-subtitle {
    border-color: rgba(0, 229, 192, 0.3);
    color: var(--cv-accent);
}
```

- [ ] **Step 2: Verify**

With the server running, open http://localhost:1313 in dark mode. Check:
- Name is larger, tighter, with a grey-to-muted-blue gradient fill
- Faint "XY" visible in the upper-right area of the header block
- Tag pill is cyan bordered
- Light mode: name is normal dark color — gradient does not apply (rule is `.dark`-scoped)

- [ ] **Step 3: Commit**

```bash
git add static/css/custom.css
git commit -m "feat: typographic drama header — gradient name and XY watermark"
```

---

## Task 3: Homepage — bio expand and section accordions

**Files:**
- Modify: `static/css/custom.css` — append to end
- Modify: `content/_index.md` — full rewrite

- [ ] **Step 1: Append bio expand and accordion CSS**

Append to end of `static/css/custom.css`:

```css
/* ============================================================
   BIO EXPAND — two-level hero card bio
   ============================================================ */

.cv-hero-bio-expand {
    margin: 0;
    max-width: 58ch;
}

.cv-hero-bio-expand > summary {
    list-style: none;
    cursor: pointer;
    color: var(--content);
    font-size: 0.94rem;
    line-height: 1.8;
    display: block;
}

.cv-hero-bio-expand > summary::-webkit-details-marker {
    display: none;
}

.cv-hero-bio-expand > summary::marker {
    display: none;
}

.cv-hero-bio-expand > summary::after {
    content: " ▸ more";
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.72rem;
    letter-spacing: 0.08em;
    color: var(--cv-accent);
}

.cv-hero-bio-expand[open] > summary::after {
    content: " ▾ less";
}

.cv-hero-bio-full {
    padding-top: 0.7rem;
}

.cv-hero-bio-full p {
    max-width: 58ch;
    color: var(--content);
    font-size: 0.9rem;
    line-height: 1.8;
    margin: 0 0 0.65rem;
}

.cv-hero-bio-full p:last-child {
    margin-bottom: 0;
}

/* ============================================================
   SECTION ACCORDIONS — <details>/<summary> as h2 replacement
   ============================================================ */

/* Counter incremented on the <details> element so summary::before reads correctly */
.cv-content details {
    counter-increment: cv-section;
}

.cv-content details > summary {
    display: flex;
    align-items: baseline;
    gap: 0.85rem;
    margin-top: 3rem;
    margin-bottom: 1rem;
    padding-bottom: 0.85rem;
    border-bottom: 1px solid var(--border);
    color: var(--primary);
    font-size: 1.4rem;
    font-weight: 650;
    letter-spacing: -0.02em;
    cursor: pointer;
    list-style: none;
}

.cv-content details > summary::-webkit-details-marker {
    display: none;
}

.cv-content details > summary::marker {
    display: none;
}

/* Numeric counter prefix — same style as .cv-content h2::before */
.cv-content details > summary::before {
    content: counter(cv-section, decimal-leading-zero);
    display: inline-block;
    color: var(--secondary);
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.74rem;
    font-weight: 500;
    letter-spacing: 0.16em;
}

/* Toggle glyph on the right */
.cv-content details > summary::after {
    content: "▸";
    margin-left: auto;
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.74rem;
    color: var(--cv-accent);
}

.cv-content details[open] > summary::after {
    content: "▾";
}

@media (max-width: 768px) {
    .cv-content details > summary {
        font-size: 1.18rem;
        gap: 0.65rem;
    }
}
```

- [ ] **Step 2: Rewrite `content/_index.md`**

Replace the entire file with the content below. Note that all content inside `<details>` is written as HTML (not markdown) to avoid Goldmark parsing issues:

```markdown
---
title: "Xiangrui Yang"
description: "PhD Student at HKU / ML Systems / Storage / HPC"
---

<div class="cv-hero">
<div class="cv-hero-text">
<div class="cv-hero-kicker">About Me</div>
<details class="cv-hero-bio-expand">
<summary>PhD @ HKU, advised by Yiming Qiu. MSc @ HUST · BSc @ SYSU. Research: ML systems, storage, HPC.</summary>
<div class="cv-hero-bio-full">
<p>PhD student @ HKU, advised by Prof. Yiming Qiu. MSc CS @ HUST (adv. Prof. Qiang Cao) · BSc CS @ SYSU (adv. Prof. Yuedong Yang).</p>
<p>Research: optimizing ML systems and HPC — CUDA, DGL, sparse matrix acceleration. Explored sparse ops in ad-ranking systems at Tencent.</p>
<p>Outside academia: economics and investment.</p>
</div>
</details>
</div>
<div class="cv-hero-photo">
<div class="cv-hero-photo-frame">
<img src="/images/user.jpg" alt="Xiangrui Yang" />
</div>
</div>
</div>

---

## Academic Papers

- [HeteroGNN: A Heterogeneous Task Division Based GNN Training Framework to Maximize CPU-GPU Parallelism](https://ieeexplore.ieee.org/document/11209980), **ICME 2025**
- [Rearchitecting Buffered I/O in the Era of High-Bandwidth SSDs](https://www.usenix.org/conference/fast26/presentation/zhan), **FAST 2026**
- ASMA: An Anisotropy Scaling Memristor-based Accelerator for LLM Inference, **ICCD 2025**
- [Rethinking the Request-to-IO Transformation Process of File Systems for Full Utilization of High-Bandwidth SSDs](https://www.usenix.org/conference/fast25/presentation/zhan), **FAST'25**
- [AIS: An Active Idleness I/O Scheduler to Reduce Buffer-Exhausted Degradation for Commodity SSDs](https://dl.acm.org/doi/10.1145/3708538), **ACM TACO**
- [RomeFS: A CXL-SSD Aware File System Exploiting Synergy of Memory-Block Dual Paths](https://dl.acm.org/doi/10.1145/3698038.3698539), **SoCC'24**
- [HEncode: A Highly Modularized and Efficient FPGA QC-LDPC Encoder Using High Level Synthesis](https://ieeexplore.ieee.org/document/10818010/), **ICCD'24**
- [A Study on Data-Layout Optimization in Memory for High-Performance Erasure Coding](http://xwxt.sict.ac.cn/CN/Y2025/V46/I4/1003)
- [Analyzing performance degradation for wide stripe erasure codes](https://www.spiedigitallibrary.org/conference-proceedings-of-spie/13067/130670E/Analyzing-performance-degradation-for-wide-stripe-erasure-codes/10.1117/12.3024709.full)
- [PMLDS: An LSM-tree Direct Managed Storage for Key-value Stores on Byte-addressable Devices](https://dl.acm.org/doi/10.1145/3605573.3605629)
- [Leveraging Orbital Information and Atomic Feature in Deep Learning Model](https://arxiv.org/abs/2211.11543)

<details>
<summary>Education</summary>
<div style="padding-top:0.5rem">
<h3><a href="https://www.hku.hk/">University of Hong Kong</a></h3>
<p><em>PhD, Computer Science</em><br><strong>2025 – present</strong> · adv. Prof. Yiming Qiu</p>
<h3>Huazhong University of Science and Technology</h3>
<p><em>MSc, Computer Science</em><br><strong>2022 – 2025</strong> · Outstanding Graduate (Top 20%)</p>
<h3>Sun Yat-sen University</h3>
<p><em>BSc, Computer Science</em><br><strong>2018 – 2022</strong></p>
</div>
</details>

<details>
<summary>Talks & Presentations</summary>
<ul style="padding-top:0.5rem">
<li>ICME'25, IEEE International Conference on Multimedia &amp; Expo 2025, Nantes, France. <a href="https://whova.com/embedded/session/hlWY6K3rL7pHvG8Yd1TfjYJVgDEZvOuEPKWGmeuUbIQ%3D/4654604/?widget=primary">Website</a></li>
<li>FAST'25, 23rd USENIX Conference on File and Storage Technologies, Santa Clara, California. <a href="https://www.youtube.com/watch?v=6dGa7Ol8Ryk">Video</a></li>
<li>SoCC'24, 15th ACM Symposium on Cloud Computing, Redmond, Washington.</li>
<li>HiPEAC'25, 20th High Performance, Edge And Cloud computing, Barcelona, Spain.</li>
</ul>
</details>

<details>
<summary>Experience</summary>
<div style="padding-top:0.5rem">
<h3><a href="https://www.tencent.com/en-us/">Tencent</a></h3>
<p><em>Advertising Engineering — Intern</em><br><strong>May 2024 – Sep 2024 &amp; Apr 2025 – Jun 2025</strong> · Shenzhen</p>
<ul>
<li>int8 quantization in ad scoring system: &gt;30% GPU kernel speedup, &gt;2% system throughput gain.</li>
<li>Added latency-analysis logs to ad recall system; tuned parameters to raise QPS from 10,000 to 15,000.</li>
</ul>
<h3><a href="https://www.sqhyfund.com/">Shengquan Hengyuan Investment</a></h3>
<p><em>Quantitative Finance Research — Intern</em><br><strong>Jun 2023 – Aug 2023</strong> · Nanjing</p>
<ul>
<li>&gt;30% annual cumulative abnormal return using high- and low-frequency signals.</li>
<li>Accelerated time-series and multi-factor model training with GPU servers.</li>
</ul>
<h3><a href="https://www.miracleplus.com/en/">Miracle Plus</a></h3>
<p><em>Investment &amp; Operations — Intern</em><br><strong>May 2023 – Jun 2023</strong> · Beijing</p>
<ul>
<li>Led diligence on a networking-industry startup that closed a Series A in the tens of millions.</li>
</ul>
<h3><a href="http://biomed.nscc-gz.cn/sail/en:research">SYSU AI4Science</a></h3>
<p><em>Data Analyst</em><br><strong>Jan 2022 – Jun 2022</strong> · Guangzhou</p>
<ul>
<li>Predicted Synthetic Lethality using random-walk + graph convolution with multi-view fusion.</li>
<li>Built message-passing models on CATL crystal database to predict physical properties.</li>
</ul>
</div>
</details>

<details>
<summary>Academic Projects</summary>
<div style="padding-top:0.5rem">
<h3>Model Optimization</h3>
<ul>
<li>Profiled DGL conv bottlenecks with Nsight; optimized GCN normalization for a 30% speedup over DGL.</li>
<li>C++/CUDA extensions for Python; CUDA operator overloading.</li>
</ul>
<h3>Reed-Solomon Code Optimization</h3>
<ul>
<li>Compared wide- vs narrow-stripe erasure codes (ISA-L / Jerasure); reached 128 Gbps single-node throughput via OpenMP.</li>
</ul>
<h3>SSD Optimization</h3>
<ul>
<li>Built SSDTEST to characterize performance degradation; developed I/O scheduler to control tail latency.</li>
</ul>
</div>
</details>

<details>
<summary>Certificates & Awards</summary>
<div style="padding-top:0.5rem">
<h3>Awards</h3>
<ul>
<li>Sangfor Scholarship (Apr. 2024)</li>
<li>HUST Scholarship, Second Prize (Oct. 2023)</li>
<li>Distinguished Activist in Community Affairs (Oct. 2023)</li>
<li>SYSU Scholarship, Second Prize (Oct. 2021)</li>
<li>2019 ACM-ICPC SYSU Competition, Second Prize (Oct. 2019)</li>
</ul>
<h3>Certificates</h3>
<ul>
<li>IELTS 7.0 · GRE 320 · TOEFL 106</li>
</ul>
</div>
</details>
```

- [ ] **Step 3: Verify bio expand and accordions**

Open http://localhost:1313:
- Hero card bio shows short text ending with `▸ more` in cyan. Click it — full bio (3 paragraphs) expands, glyph becomes `▾ less`.
- Academic Papers (`h2`) is fully visible, counter shows `01`.
- Education, Talks, Experience, Projects, Certificates show as collapsed headings with `▸` on the right and counters `02`–`06`. Click any — content expands.
- Counters are in document order: Papers=01, Education=02, Talks=03, Experience=04, Projects=05, Certificates=06.

- [ ] **Step 4: Commit**

```bash
git add static/css/custom.css content/_index.md
git commit -m "feat: compress homepage — bio expand and section accordions"
```

---

## Task 4: Blog list — Compact List layout

**Files:**
- Modify: `static/css/custom.css` — append to end
- Create: `layouts/_default/list.html`

- [ ] **Step 1: Append blog list CSS**

Append to end of `static/css/custom.css`:

```css
/* ============================================================
   BLOG LIST — Compact List
   ============================================================ */

.list-page {
    position: relative;
    isolation: isolate;
    max-width: 980px;
    margin: 0 auto;
    padding: 3rem 1.4rem 4.5rem;
}

/* Grid backdrop — same pattern as homepage */
.list-page::after {
    content: "";
    position: absolute;
    inset: 0;
    background-image:
        linear-gradient(var(--cv-grid) 1px, transparent 1px),
        linear-gradient(90deg, var(--cv-grid) 1px, transparent 1px);
    background-position: center top;
    background-size: 32px 32px;
    opacity: 0.28;
    pointer-events: none;
    z-index: -1;
    -webkit-mask-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.22), transparent 26%);
    mask-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.22), transparent 26%);
}

/* Page heading styled like homepage h2 */
.list-page-header {
    display: flex;
    align-items: baseline;
    gap: 0.85rem;
    margin-bottom: 2.5rem;
    padding-bottom: 0.85rem;
    border-bottom: 1px solid var(--border);
    color: var(--primary);
    font-size: 1.4rem;
    font-weight: 650;
    letter-spacing: -0.02em;
}

.list-page-header::before {
    content: "01";
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.74rem;
    font-weight: 500;
    letter-spacing: 0.16em;
    color: var(--secondary);
}

/* Each post entry */
.post-entry-link {
    display: block;
    text-decoration: none;
    color: inherit;
    padding: 1.1rem 0;
    border-bottom: 1px solid var(--border);
    transition: opacity 0.15s ease;
}

.post-entry-link:hover .post-entry-title {
    color: var(--cv-accent);
}

.post-entry-meta {
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.72rem;
    color: var(--secondary);
    letter-spacing: 0.08em;
    margin-bottom: 0.2rem;
}

.post-entry-title {
    font-size: 1rem;
    font-weight: 600;
    letter-spacing: -0.02em;
    color: var(--primary);
    margin: 0 0 0.25rem;
    line-height: 1.4;
    transition: color 0.15s ease;
}

.post-entry-cats {
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.68rem;
    color: var(--cv-accent);
    letter-spacing: 0.06em;
    margin-bottom: 0.25rem;
}

.post-entry-summary {
    font-size: 0.88rem;
    color: var(--content);
    line-height: 1.65;
    margin: 0;
    max-width: 70ch;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

@media (max-width: 768px) {
    .list-page {
        padding: 1.5rem 1rem 3rem;
    }

    .list-page::after {
        opacity: 0.18;
    }

    .list-page-header {
        font-size: 1.18rem;
        gap: 0.65rem;
    }
}
```

- [ ] **Step 2: Create `layouts/_default/list.html`**

```html
{{- define "main" }}
<div class="list-page">
    {{- if .Title }}
    <h1 class="list-page-header">{{ .Title }}</h1>
    {{- end }}

    {{- $pages := union .RegularPages .Sections }}
    {{- $paginator := .Paginate $pages }}

    {{- range $paginator.Pages }}
    <a class="post-entry-link" href="{{ .Permalink }}">
        <div class="post-entry-meta">{{ .Date.Format "2006-01-02" }}</div>
        <h2 class="post-entry-title">{{ .Title }}</h2>
        {{- with .Params.categories }}
        <div class="post-entry-cats">{{ delimit . " · " }}</div>
        {{- end }}
        {{- if .Summary }}
        <p class="post-entry-summary">{{ .Summary | plainify | htmlUnescape }}</p>
        {{- end }}
    </a>
    {{- end }}

    {{- if gt $paginator.TotalPages 1 }}
    <footer class="page-footer">
        <nav class="pagination">
            {{- if $paginator.HasPrev }}
            <a class="prev" href="{{ $paginator.Prev.URL | absURL }}">« {{ i18n "prev_page" }}</a>
            {{- end }}
            {{- if $paginator.HasNext }}
            <a class="next" href="{{ $paginator.Next.URL | absURL }}">{{ i18n "next_page" }} »</a>
            {{- end }}
        </nav>
    </footer>
    {{- end }}
</div>
{{- end }}
```

- [ ] **Step 3: Verify blog list**

Open http://localhost:1313/blog/:
- Faint grid backdrop visible, fades downward
- "Blog" heading has `01` monospace counter prefix and bottom border
- Each post: date (dim) → title (heading color) → category label (cyan) → 2-line excerpt (body grey)
- Hover a post: title turns cyan
- No card borders or shadows — only a bottom divider line per entry

- [ ] **Step 4: Commit**

```bash
git add static/css/custom.css layouts/_default/list.html
git commit -m "feat: compact list layout for blog index"
```

---

## Task 5: Article page — Lab Notebook layout

**Files:**
- Modify: `static/css/custom.css` — append to end
- Create: `layouts/_default/single.html`

- [ ] **Step 1: Append Lab Notebook CSS**

Append to end of `static/css/custom.css`:

```css
/* ============================================================
   ARTICLE PAGE — Lab Notebook
   ============================================================ */

.lab-page {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 2.5rem;
    max-width: 1080px;
    margin: 0 auto;
    padding: 3rem 1.4rem 4.5rem;
    position: relative;
    isolation: isolate;
}

/* Grid backdrop */
.lab-page::after {
    content: "";
    position: absolute;
    inset: 0;
    background-image:
        linear-gradient(var(--cv-grid) 1px, transparent 1px),
        linear-gradient(90deg, var(--cv-grid) 1px, transparent 1px);
    background-position: center top;
    background-size: 32px 32px;
    opacity: 0.28;
    pointer-events: none;
    z-index: -1;
    -webkit-mask-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.22), transparent 20%);
    mask-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.22), transparent 20%);
}

/* ---- Sidebar ---- */

.lab-sidebar {
    position: sticky;
    top: 5rem;
    height: fit-content;
    max-height: calc(100vh - 6rem);
    overflow-y: auto;
    scrollbar-width: none;
}

.lab-sidebar::-webkit-scrollbar {
    display: none;
}

.lab-breadcrumb {
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.72rem;
    letter-spacing: 0.06em;
    color: var(--secondary);
    margin-bottom: 1.2rem;
}

.lab-breadcrumb a {
    color: var(--secondary);
    text-decoration: none;
    transition: color 0.15s;
}

.lab-breadcrumb a:hover {
    color: var(--cv-accent);
}

/* TOC generated by Hugo — targets the <nav> Hugo emits */
.lab-toc {
    margin-bottom: 1.5rem;
}

.lab-toc nav ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.lab-toc nav li {
    margin: 0;
}

.lab-toc nav a {
    display: block;
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.68rem;
    color: var(--secondary);
    text-decoration: none;
    line-height: 2;
    padding-left: 0.5rem;
    border-left: 2px solid transparent;
    transition: color 0.15s, border-color 0.15s;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.lab-toc nav a:hover {
    color: var(--primary);
}

.lab-toc nav a.active {
    color: var(--cv-accent);
    border-left-color: var(--cv-accent);
}

/* h3-level TOC items — indent */
.lab-toc nav ul ul {
    padding-left: 0.6rem;
}

.lab-meta {
    font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
    font-size: 0.68rem;
    color: var(--secondary);
    letter-spacing: 0.06em;
    line-height: 2;
}

.lab-tag {
    color: var(--cv-accent);
}

/* ---- Article header ---- */

.lab-header {
    margin-bottom: 2rem;
}

.lab-header h1 {
    font-size: clamp(2rem, 5vw, 2.8rem);
    font-weight: 700;
    letter-spacing: -0.04em;
    line-height: 1.1;
    margin: 0;
    color: var(--primary);
}

.dark .lab-header h1 {
    background: linear-gradient(100deg, #dde2ec 30%, #6a80b0 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

/* ---- Article body headings ---- */

.lab-content.post-content h2 {
    display: flex;
    align-items: baseline;
    gap: 0.75rem;
    margin-top: 2.5rem;
    margin-bottom: 0.85rem;
    padding-bottom: 0.75rem;
    border-bottom: 1px solid var(--border);
    color: var(--primary);
    font-size: 1.25rem;
    font-weight: 650;
    letter-spacing: -0.02em;
}

.lab-content.post-content h3 {
    position: relative;
    margin-top: 1.6rem;
    margin-bottom: 0.4rem;
    padding-left: 1rem;
    color: var(--primary);
    font-size: 1.05rem;
    letter-spacing: -0.01em;
}

.lab-content.post-content h3::before {
    content: "";
    position: absolute;
    left: 0;
    top: 0.2rem;
    bottom: 0.2rem;
    width: 2px;
    border-radius: 999px;
    background: linear-gradient(180deg, var(--cv-accent), transparent);
}

/* ---- Mobile ---- */

@media (max-width: 768px) {
    .lab-page {
        grid-template-columns: 1fr;
        gap: 0;
        padding: 1.5rem 1rem 3rem;
    }

    .lab-sidebar {
        position: static;
        max-height: none;
        display: none;
    }

    .lab-mobile-meta {
        display: flex;
        gap: 0.75rem;
        font-family: "SF Mono", "JetBrains Mono", "IBM Plex Mono", monospace;
        font-size: 0.7rem;
        color: var(--secondary);
        letter-spacing: 0.06em;
        margin-bottom: 0.75rem;
    }

    .lab-mobile-meta .lab-tag {
        color: var(--cv-accent);
    }
}

@media (min-width: 769px) {
    .lab-mobile-meta {
        display: none;
    }
}
```

- [ ] **Step 2: Create `layouts/_default/single.html`**

```html
{{- define "main" }}
<div class="lab-page">
    <aside class="lab-sidebar">
        <div class="lab-breadcrumb">
            <a href="/blog/">~/blog</a>&nbsp;/
        </div>

        {{- with .TableOfContents }}
        <div class="lab-toc">
            {{ . }}
        </div>
        {{- end }}

        <div class="lab-meta">
            <div class="lab-date">{{ .Date.Format "2006-01-02" }}</div>
            {{- with .Params.categories }}
            <div>{{- range . }}<span class="lab-tag">{{ . }}</span> {{- end }}</div>
            {{- end }}
        </div>
    </aside>

    <article class="lab-content post-content">
        {{/* Mobile-only meta — shown above title on small screens */}}
        <div class="lab-mobile-meta">
            <span>{{ .Date.Format "2006-01-02" }}</span>
            {{- with .Params.categories }}
            {{- range . }}<span class="lab-tag">{{ . }}</span>{{- end }}
            {{- end }}
        </div>

        <header class="lab-header">
            <h1>{{ .Title }}</h1>
        </header>

        {{ .Content }}
    </article>
</div>

<script>
(function () {
    var tocLinks = document.querySelectorAll('.lab-toc nav a');
    if (!tocLinks.length) return;

    var headings = document.querySelectorAll('.lab-content h2, .lab-content h3');
    if (!headings.length) return;

    var observer = new IntersectionObserver(function (entries) {
        entries.forEach(function (entry) {
            if (!entry.isIntersecting) return;
            var id = entry.target.getAttribute('id');
            if (!id) return;
            tocLinks.forEach(function (l) { l.classList.remove('active'); });
            var match = document.querySelector('.lab-toc nav a[href="#' + id + '"]');
            if (match) match.classList.add('active');
        });
    }, {
        rootMargin: '-10% 0px -80% 0px',
        threshold: 0
    });

    headings.forEach(function (h) { observer.observe(h); });
}());
</script>
{{- end }}
```

- [ ] **Step 3: Verify article layout**

Open http://localhost:1313/blog/fed/ (or any post with headings):
- Two-column layout: 200px sidebar on left, article prose on right
- Sidebar: `~/blog /` breadcrumb, TOC links (dim, monospace), date + category below
- Scroll through the article — active TOC link turns cyan with left border
- Article `h1` has gradient fill in dark mode
- `h2` has bottom border; `h3` has cyan left accent bar
- Resize browser to ≤768px: sidebar disappears, date/category appear above the title inline

- [ ] **Step 4: Commit**

```bash
git add static/css/custom.css layouts/_default/single.html
git commit -m "feat: lab notebook layout for article pages with scroll-spy TOC"
```

---

## Task 6: Final build verification

**Files:** none changed

- [ ] **Step 1: Full Hugo build**

```bash
hugo
```

Expected: exits with no errors. Output goes to `../yxr_public`. If there are template errors they appear as:
```
Error: ... execute of template failed: ...
```
Fix before continuing.

- [ ] **Step 2: Cross-check all three pages in dark mode**

With `hugo server -D` running:

| URL | What to verify |
|---|---|
| http://localhost:1313 | Gradient name, XY watermark, cyan pill, bio expand (`▸ more`), section accordions with counters |
| http://localhost:1313/blog/ | Grid backdrop, `01 Blog` header, compact entries with date/category/excerpt, hover turns title cyan |
| http://localhost:1313/blog/fed/ | Sidebar TOC, breadcrumb, sticky on scroll, scroll-spy highlights, gradient h1, mobile collapses sidebar |

- [ ] **Step 3: Light mode regression check**

Toggle to light mode on each page. Verify:
- No gradient text on homepage name (gradient is `.dark`-scoped)
- No XY watermark (also `.dark`-scoped)
- Tag pill returns to grey border (`.dark .cv-subtitle` rule only applies in dark)
- Blog list and article pages read normally with the existing light palette

- [ ] **Step 4: Final commit**

```bash
git add -A
git commit -m "feat: complete Graphite Lab UI redesign

- Dark palette: #111318 bg, #00e5c0 accent, updated PaperMod base tokens
- Homepage: typographic drama header, gradient name, XY watermark
- Homepage: bio expand via <details>, section accordions for all secondary sections
- Blog list: compact list layout with shared grid backdrop
- Article page: lab notebook sticky sidebar, scroll-spy TOC, gradient h1"
```
