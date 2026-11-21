# Week 10 — Keep Building: Portfolio Maintenance

**Author:** Arya Vengurlekar
**Portfolio URL:** `https://aryavengurlekar03.github.io/Machine-Learning/`
**GitHub Repository:** `https://github.com/AryaVengurlekar03/Machine-Learning`
**Date:** November 21, 2026

---

## 1. Where the Next Case Study Goes

My portfolio is a single-page website served from `index.html` at the repository root via GitHub Pages. All projects are displayed inside the **"Featured Projects & Case Studies"** section, identified by `<section id="work">`.

### Portfolio project listing section

The `<section id="work">` block in `index.html` contains a `section-header` with the title **"Featured Projects & Case Studies"**, followed by individual `<article class="project-card">` blocks — one per project. The section currently holds three project cards:

| # | Project | Card class | Location in `index.html` |
|---|---------|------------|--------------------------|
| 1 | FlyRank Search Content Refresh Opportunity Model | `project-card featured` | Lines ~760–800 |
| 2 | Binance Futures Algorithmic Trading Bot | `project-card` | Lines ~802–824 |
| 3 | E-Commerce Customer Segmentation Analysis | `project-card` | Lines ~826–848 |

The next case study card will be inserted as a new `<article class="project-card">` block after the last existing `</article>` tag and before the `</section>` closing tag at line ~849.

### HTML file where the project card should be added

**`index.html`** (repository root) — inside `<section id="work">`.

If the case study warrants a full standalone write-up page (similar to the existing `paper.html` research paper), create a new HTML file at the repository root (e.g., `quantum-autoencoder.html`) and link to it from the project card.

### Supporting files and folders

| Content type | Destination path |
|-------------|-----------------|
| Jupyter notebooks | `work/notebooks/` (e.g., `work/notebooks/quantum_autoencoder.ipynb`) |
| Generated figures & charts | `work/figures/` |
| Python scripts | `scripts/` |
| Documentation & case study write-up | `docs/` |
| Pipeline outputs & exports | `work/outputs/` or `outputs/` |
| Standalone HTML write-up | Repository root (e.g., `quantum-autoencoder.html`) |

### CSS and design structure to follow

All styles are defined inline within the `<style>` block in `index.html`. The design system uses these CSS custom properties:

| Variable | Value | Purpose |
|----------|-------|---------|
| `--font-family` | `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif` | Primary typeface |
| `--accent` | `#2563EB` | Link color, badges, metric values |
| `--accent-hover` | `#1D4ED8` | Hover state for links and buttons |
| `--accent-light` | `#EFF6FF` | Tag/badge backgrounds |
| `--bg` | `#F8FAFC` | Page background |
| `--card-bg` | `#FFFFFF` | Card backgrounds |
| `--text-primary` | `#0F172A` | Headings |
| `--text-secondary` | `#334155` | Body text |
| `--text-muted` | `#64748B` | Captions and labels |
| `--border-color` | `#E2E8F0` | Card borders |
| `--shadow-sm` | `0 1px 2px 0 rgba(0,0,0,0.05)` | Card shadow |

Cards use `border-radius: 0.875rem`, padding of `1.75rem`, and `margin-bottom: 1.5rem`. Technology labels use the `tech-pill` class (`background: #F1F5F9; color: #475569; border-radius: 0.375rem`). The mobile breakpoint is `@media (max-width: 640px)`.

A standalone HTML page should include the same `<style>` block, `<nav class="nav-bar">` navigation, and `<footer>` as `index.html` for visual consistency.

### Navigation and sitemap changes

- **Navigation bar (`index.html`, lines ~719–727):** If a standalone HTML page is created for the case study, add a `<li><a href="quantum-autoencoder.html">` entry inside the `<ul class="nav-links">` block. If the project is only a card within `<section id="work">`, no nav changes are needed — the existing `<a href="#work">Work</a>` link already covers it.
- **Sitemap (`sitemap.xml`):** Add a new `<url>` entry for any standalone HTML page. The sitemap currently lists `index.html` and `resume.html`.
- **Open Graph metadata:** Any new standalone page should include `og:title`, `og:description`, `og:type`, and `og:url` meta tags matching the existing pattern in `index.html`.

---

## 2. My Case Study Format

Every case study follows the **three-beat structure** established in Week 2:

### Problem

- What problem was I trying to solve?
- Who experiences this problem and is affected by it?
- Why does it matter — what is the cost of leaving it unsolved?

State the real-world pain point, name the audience (users, teams, researchers, stakeholders), and explain why existing approaches are insufficient.

### What I Did

- What approach did I take (methodology, architecture, pipeline)?
- What tools, technologies, models, and methods did I use?
- What important technical decisions did I make, and why?
- How did I validate my results to ensure they were honest and reproducible?

Describe the full implementation: data sources, feature engineering, model selection, evaluation strategy, and key trade-offs.

### What Came of It

- What results did I achieve (specific metrics, quantitative evidence)?
- What worked and what didn't?
- What did I learn from building this?
- What would I improve or do differently next time?

Present results honestly, acknowledge limitations, and identify concrete next steps.

---

### Reusable Copy-Paste Template

```markdown
# [Project Title]

**Status:** [Completed / In Progress / Planned]
**Date:** [Month Year]
**Repository:** [GitHub URL]
**Live Demo:** [URL or N/A]

---

## Problem

<!-- What problem was I trying to solve? Who needed it and why? -->

[Describe the real-world problem in 2–3 sentences. Name the specific
audience affected. Explain why existing solutions are insufficient
or why this problem matters.]

---

## What I Did

<!-- What approach, tools, decisions, and implementation did I use? -->

**Approach:** [1–2 sentence methodology summary]

**Tech Stack:**
- [Language / framework]
- [Libraries / tools]
- [Data source]

**Key Technical Decisions:**
1. [Decision and rationale]
2. [Decision and rationale]
3. [Decision and rationale]

**Validation Strategy:** [How I ensured honest, reproducible results —
e.g., holdout split, cross-validation, leakage audit]

---

## What Came of It

<!-- Results, lessons, limitations, and next steps -->

**Results:**
| Metric | Value |
|--------|-------|
| [Metric 1] | [Value] |
| [Metric 2] | [Value] |

**What Worked:** [Key successes]

**What Didn't:** [Honest limitations and shortcomings]

**What I Learned:** [Main takeaways from building this]

**Next Steps:** [Concrete improvements or follow-up work]
```

---

## 3. Steps to Add My Next Case Study

1. **Identify the problem and target audience.** Write a one-sentence problem statement and name who benefits. This becomes the `<p class="project-desc">` paragraph in the project card in `index.html`.

2. **Gather project evidence.** Collect all supporting artifacts before writing:
   - Screenshots and exported charts → save to `work/figures/`
   - Architecture or pipeline diagrams → save to `work/figures/`
   - Quantitative results and metrics → export from notebooks in `work/notebooks/`
   - Demo recording or live URL → note the link
   - Repository URL → confirm the repo is public and its `README.md` is up to date

3. **Write the case study using the three-beat format.** Copy the template from Section 2. Fill in the Problem, What I Did, and What Came of It sections with real evidence. Save the Markdown write-up to `docs/` (e.g., `docs/QUANTUM_AUTOENCODER_CASE_STUDY.md`). If a full HTML write-up page is warranted, create it at the repository root following the structure of `paper.html`.

4. **Create the project page or content.** If the project needs its own detailed HTML page (like `paper.html`), create it at the repository root (e.g., `quantum-autoencoder.html`). Reuse the `<style>` block, `<nav class="nav-bar">`, and `<footer>` from `index.html` to maintain visual consistency. If the project only needs a portfolio card, skip this step.

5. **Add the project card to the portfolio listing in `index.html`.** Insert a new `<article class="project-card">` block inside `<section id="work">`, after the last existing `</article>` and before the closing `</section>` tag. Follow this HTML structure:

   ```html
   <article class="project-card">
       <div class="project-header">
           <span class="project-tag">[CATEGORY]</span>
           <span style="font-size: 0.8125rem; color: #64748B; font-weight: 500;">[Date]</span>
       </div>
       <h3 class="project-title">[Project Title]</h3>
       <p class="project-desc">
           [One-paragraph project description from Beat 1 — Problem]
       </p>

       <div class="metrics-grid">
           <div class="metric-item">
               <span class="metric-val">[Value]</span>
               <span class="metric-lbl">[Metric Label]</span>
           </div>
       </div>

       <div class="tech-pills">
           <span class="tech-pill">[Tech 1]</span>
           <span class="tech-pill">[Tech 2]</span>
       </div>

       <a href="[CASE_STUDY_URL]" class="project-link">
           [Link Text] →
       </a>
   </article>
   ```

6. **Match the existing typography, colors, spacing, and design system.** Use the CSS custom properties documented in Section 1: Inter font via `var(--font-family)`, accent blue `#2563EB`, card background `#FFFFFF` with `border-radius: 0.875rem`, and tech pills with `background: #F1F5F9`. Do not introduce new fonts, colors, or spacing values that break visual consistency.

7. **Ensure mobile responsiveness.** Verify the new card renders correctly at the 375px viewport width defined by the existing `@media (max-width: 640px)` breakpoint in `index.html`. Check for: no horizontal overflow, navigation wrapping cleanly, touch targets ≥ 44px, and readable text without zooming.

8. **Test all images, repository links, demo links, and navigation.** Manually verify each link and asset:
   - [ ] All `href` values resolve without 404 errors
   - [ ] All images in `work/figures/` load correctly and are committed to Git
   - [ ] Repository link points to the correct public GitHub repo
   - [ ] Demo URL works or is explicitly marked N/A
   - [ ] Internal anchor links (`#work`, `#about`, etc.) scroll correctly
   - [ ] Any standalone page link in the nav bar works

9. **Update sitemap and metadata if required.** If a standalone HTML page was created:
   - Add a `<url>` entry in `sitemap.xml` with the correct `<loc>`, `<lastmod>`, and `<priority>` values.
   - Ensure the new page has `<meta name="description">`, `<meta property="og:title">`, `<meta property="og:description">`, and `<link rel="canonical">` tags.

10. **Review everything before publishing.** Read the full project card and case study end to end. Confirm the three-beat format is complete, all metrics are real and accurate, no placeholder text remains, and no fabricated results are included. Only then commit and push.

---

## 4. Next Project I Intend to Add

**Title:** Quantum Autoencoder for Anomaly Detection in Satellite Imagery

**Status:** 🟡 **PLANNED / IN PROGRESS**

**Description:** A quantum machine learning project exploring the use of quantum autoencoders for anomaly detection in satellite imagery. The project will investigate whether quantum autoencoder circuits can learn compressed latent representations of satellite image patches and use reconstruction error to identify anomalous regions — such as deforestation events, urban expansion, infrastructure damage, or environmental anomalies. This sits at the intersection of quantum computing, computer vision, and remote sensing.

**Anticipated Tech Stack:** Python, PennyLane or Qiskit, PyTorch or TensorFlow, satellite imagery datasets (e.g., EuroSAT, Sentinel-2), scikit-learn, Matplotlib.

**What is not claimed:**
- The project is **not complete**.
- No accuracy, precision, recall, F1, or any other evaluation metric is available yet.
- No experiments have been run to completion.
- No screenshots, architecture diagrams, or demo recordings exist yet.
- No results have been fabricated or estimated.

**When this case study will be added to the portfolio:** Only after the project has reached a substantial milestone with:
- Working, tested code in a public GitHub repository
- Real evaluation results from actual experiments
- Figures, charts, or screenshots demonstrating the implementation
- A complete three-beat write-up based on genuine evidence

No placeholder card will be added to `index.html` until all of the above exist.

---

## 5. Preserving My Build Context

I will continue using my existing **Claude Project** for all future portfolio development work. This project already contains my established working context for:

- **Personal writing voice:** Professional, technical, and honest about both results and limitations. Direct claims backed by evidence; no vague superlatives or unsubstantiated marketing language.
- **Technical background and stack:** Python, scikit-learn, pandas, DuckDB, HTML/CSS/JS, the design system in `index.html` (Inter font, CSS custom properties, card-based layout), and the GitHub Pages deployment workflow.
- **Professional identity and career direction:** Computer Science student, Machine Learning Intern at FlyRank, specializing in search intelligence, position-aware ranking, and decision-support ML.
- **Portfolio design and visual preferences:** Color palette (`--accent: #2563EB`, `--bg: #F8FAFC`, `--text-primary: #0F172A`), card styling with `border-radius: 0.875rem`, section headers with uppercase titles and bottom borders, `tech-pill` badge layout, `metrics-grid` for quantitative highlights, and mobile-first responsive design.
- **Existing project context and case study format:** The FlyRank capstone structure (problem → methodology → results → limitations), the three-beat format (Problem → What I Did → What Came of It), and engineering principles (decision-first framing, leakage prevention, honest out-of-sample evaluation).

**Purpose:** By preserving this project context, I avoid rebuilding my voice, design decisions, structural patterns, and professional framing from scratch every time I add a new case study. I open the existing Claude Project, use the three-beat template, and write within the established framework.

> **Note:** No secrets, API keys, tokens, credentials, or sensitive personal information are stored in or required by this context. The Claude Project contains only portfolio structure, design preferences, writing voice conventions, and professional context.

---

## 6. Reminder Details

| Field | Value |
|-------|-------|
| **Reminder Title** | Add Next Portfolio Case Study |
| **Reminder Date** | December 1, 2026, at 10:00 AM |
| **Reminder Description** | Review my portfolio and add the *Quantum Autoencoder for Anomaly Detection in Satellite Imagery* case study once the project has reached a substantial milestone and I have actual results, screenshots, and implementation evidence. |

**⚠️ Important:** This is a written reminder record inside this documentation file only. **No real calendar event, system notification, phone alert, or automated reminder has been created.** The actual reminder must be set separately using a personal calendar, task manager, or reminder application.

---

*Document created: November 21, 2026*
*Repository: `https://github.com/AryaVengurlekar03/Machine-Learning`*
*File: `docs/WEEK10_PORTFOLIO_MAINTENANCE.md`*
