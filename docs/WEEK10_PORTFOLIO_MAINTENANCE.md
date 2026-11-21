# Week 10 — Portfolio Maintenance & Future Case Studies

**Author:** Arya Vengurlekar
**Portfolio URL:** `https://aryavengurlekar03.github.io/Machine-Learning/`
**GitHub Repository:** `https://github.com/AryaVengurlekar03/Machine-Learning`
**Date:** November 21, 2026

---

## 1. Where the Next Case Study Will Go

The portfolio is a single-page site served from `index.html` at the repository root via GitHub Pages. All projects live in the **"Featured Projects & Case Studies"** section (`<section id="work">`), which currently contains three `<article class="project-card">` blocks:

| # | Project | Card class | Lines in `index.html` |
|---|---------|------------|-----------------------|
| 1 | FlyRank Search Content Refresh Opportunity Model | `project-card featured` | ~760–800 |
| 2 | Binance Futures Algorithmic Trading Bot | `project-card` | ~802–824 |
| 3 | E-Commerce Customer Segmentation Analysis | `project-card` | ~826–848 |

**Where the next case study goes:**

- **Portfolio website (`index.html`):** Add a new `<article class="project-card">` block inside the `<section id="work">` container, after the existing three project cards and before the closing `</section>` tag (currently at line ~849). Follow the same HTML structure used by the existing cards (project-header, project-tag, project-title, project-desc, tech-pills, project-link).

- **GitHub repository:** The project's code, notebooks, and data belong in the existing directory structure:
  - Notebooks → `work/notebooks/` (e.g., `work/notebooks/quantum_autoencoder.ipynb`)
  - Figures/charts → `work/figures/`
  - Scripts → `scripts/`
  - Documentation → `docs/`
  - If the project warrants a standalone HTML write-up (like `paper.html`), place it at the repository root alongside the existing pages.

- **Sitemap (`sitemap.xml`):** Add a `<url>` entry for any new standalone HTML page.

- **Navigation (`index.html` nav bar):** If the case study gets its own HTML page, add a link in the `<ul class="nav-links">` block (lines ~719–727). Otherwise, the `#work` anchor already covers it.

---

## 2. The Three-Beat Case Study Format

Every case study follows this structure, adapted from the Week 2 problem-framing methodology:

### Beat 1 — Problem

What problem was I trying to solve? Who needed it solved, and why did it matter?

- State the real-world pain point or opportunity.
- Identify the specific audience (team, users, stakeholders).
- Explain why existing solutions were insufficient.

### Beat 2 — What I Did

What approach, tools, technical decisions, and implementation did I use?

- Describe the methodology, architecture, and key design choices.
- List the technology stack and frameworks used.
- Explain critical trade-offs and why I made them.
- Note the validation strategy and how I ensured honest results.

### Beat 3 — What Came of It

What was the result? What worked, what didn't, and what did I learn?

- Present quantitative results with specific metrics.
- Acknowledge limitations and what fell short.
- State what I would do differently next time.
- Identify concrete next steps or future work.

---

### Copy-Paste Template

```markdown
# [Project Title]

**Status:** [Completed / In Progress / Planned]
**Date:** [Month Year]
**Repository:** [GitHub URL]
**Live Demo:** [URL or "N/A"]

---

## Problem

<!-- What problem was I trying to solve? Who needed it and why? -->

[Describe the real-world problem. Who is affected? Why do existing
approaches fail or fall short?]

---

## What I Did

<!-- What approach, tools, technical decisions, and implementation did I use? -->

**Approach:** [Methodology summary — e.g., supervised learning, quantum
circuit design, unsupervised clustering]

**Tech Stack:** [e.g., Python, PennyLane, scikit-learn, TensorFlow Quantum]

**Key Decisions:**
- [Decision 1 and rationale]
- [Decision 2 and rationale]

**Validation Strategy:** [How I ensured honest, reproducible results]

---

## What Came of It

<!-- What was the result? What worked, what didn't, and what did I learn? -->

**Results:**
- [Metric 1]: [Value]
- [Metric 2]: [Value]

**What Worked:** [Summarize successes]

**What Didn't:** [Acknowledge limitations honestly]

**What I Learned:** [Key takeaways]

**Next Steps:** [Future improvements or follow-up work]
```

---

## 3. Exact Steps to Add a Future Project

1. **Identify the problem and target audience.** Write one sentence stating the problem and one sentence naming who benefits. This becomes the project-desc paragraph in the card.

2. **Gather project evidence.** Collect all artifacts before writing:
   - Screenshots or exported figures → save to `work/figures/`
   - Architecture diagrams → save to `work/figures/` or embed inline
   - Quantitative results (metrics, tables) → export from notebooks
   - Demo recording or live URL → note the link
   - Repository URL → confirm it is public and the README is current

3. **Write the case study using the three-beat format.** Use the copy-paste template from Section 2 above. Write the Problem, What I Did, and What Came of It sections. Save the write-up to `docs/` (e.g., `docs/QUANTUM_AUTOENCODER_CASE_STUDY.md`). If the case study warrants a full HTML page, create it at the repo root following the design patterns in `paper.html`.

4. **Add a project card to `index.html`.** Insert a new `<article class="project-card">` block inside `<section id="work">`, after the last existing `</article>` and before `</section>`. Use the existing card HTML structure:
   ```html
   <article class="project-card">
       <div class="project-header">
           <span class="project-tag">[CATEGORY TAG]</span>
           <span style="font-size: 0.8125rem; color: #64748B; font-weight: 500;">[Date or Status]</span>
       </div>
       <h3 class="project-title">[Project Title]</h3>
       <p class="project-desc">[One-paragraph description]</p>
       <div class="tech-pills">
           <span class="tech-pill">[Tech 1]</span>
           <span class="tech-pill">[Tech 2]</span>
       </div>
       <a href="[LINK]" class="project-link">[Link Text] →</a>
   </article>
   ```

5. **Link the project from navigation if it has its own page.** If you created a standalone HTML page (e.g., `quantum-autoencoder.html`), add a `<li><a href="quantum-autoencoder.html">` entry inside the `<ul class="nav-links">` block in `index.html` (lines ~719–727). Update `sitemap.xml` with a new `<url>` entry.

6. **Match the existing design system and mobile layout.** Use the same CSS variables defined in `index.html`:
   - Font: `Inter` via `var(--font-family)`
   - Colors: `--accent: #2563EB`, `--text-primary: #0F172A`, `--text-secondary: #334155`
   - Card style: `--card-bg`, `--border-color`, `--shadow-sm` with `border-radius: 0.875rem`
   - Mobile breakpoint: `@media (max-width: 640px)` — verify no horizontal overflow at 375px viewport width

7. **Verify every link, image, repository, and demo.** Check each one manually:
   - [ ] All `href` values resolve (no 404s)
   - [ ] All images load (`work/figures/` paths are correct and files are committed)
   - [ ] Repository link points to the correct public repo
   - [ ] Demo URL works (or is marked N/A)
   - [ ] `sitemap.xml` entries are valid if a new page was added

8. **Review the final case study before publishing.** Read the full card and case study write-up end to end. Confirm the three-beat format is complete, metrics are accurate, and no placeholder text remains. Commit and push only after this review pass.

---

## 4. Next Planned Project

**Title:** Quantum Autoencoder for Anomaly Detection in Satellite Imagery

**Status:** 🟡 Planned / In Progress — not yet completed. No results, metrics, or implementation evidence are available yet.

**Brief Description:** This project will explore quantum machine learning applied to anomaly detection in satellite imagery. The goal is to design and train a quantum autoencoder circuit capable of learning compressed representations of satellite image patches, then using reconstruction error to flag anomalous regions (e.g., deforestation events, infrastructure changes, or environmental anomalies). The project sits at the intersection of quantum computing, computer vision, and remote sensing.

**Anticipated Tech Stack:** Python, PennyLane or Qiskit, PyTorch/TensorFlow, satellite imagery datasets (e.g., EuroSAT, Sentinel-2), scikit-learn.

**When it will be added to the portfolio:** Only after the project reaches a substantial milestone with real, verified results, working code in a public repository, and actual figures or screenshots demonstrating the implementation. No placeholder card will be added to `index.html` until evidence exists.

---

## 5. Preserving Build Context

I will continue using my existing **Claude Project** for all future portfolio work. This project already has established context for:

- **Voice and tone:** Professional, technical, honest about results and limitations.
- **Technology stack:** The HTML/CSS design system in `index.html` (Inter font, CSS custom properties, card-based layout, mobile-first responsive breakpoints).
- **Personal identity details:** Name, role, university, internship at FlyRank, GitHub and LinkedIn profile URLs — all already present in the portfolio.
- **Visual design preferences:** Color palette (`--accent: #2563EB`, `--bg: #F8FAFC`, `--text-primary: #0F172A`), card styling, section headers with uppercase titles and bottom borders, tech pill badges, metric grids.
- **Portfolio architecture:** Single-page `index.html` with anchor sections (`#work`, `#about`, `#skills`, `#contact`), standalone pages for detailed write-ups (`paper.html`, `resume.html`), and GitHub Pages deployment.
- **Engineering principles:** Decision-first framing, strict leakage prevention, honest claims backed by out-of-sample evaluation.

By preserving this project context, I avoid rebuilding voice, design, and structural decisions from scratch every time I add a new case study. I open the existing Claude Project, paste the three-beat template, and write within the established framework.

> **Note:** No secrets, API keys, tokens, credentials, or sensitive personal information are stored in or required by this context. The Claude Project contains only portfolio structure, design preferences, and writing conventions.

---

## 6. Reminder Record

| Field | Value |
|-------|-------|
| **Reminder Title** | Add Next Portfolio Case Study |
| **Suggested Date** | November 4, 2026 |
| **Message** | Review my portfolio and add the *Quantum Autoencoder for Anomaly Detection in Satellite Imagery* case study once the project has reached a substantial milestone and I have actual results, screenshots, and implementation evidence. |

**⚠️ Important:** This is a written record only. No calendar event, system notification, or automated reminder has been created. I will set the actual reminder separately using my own calendar or task management tool.

---

*Document created: November 21, 2026*
*Repository: `https://github.com/AryaVengurlekar03/Machine-Learning`*
*File: `docs/WEEK10_PORTFOLIO_MAINTENANCE.md`*
