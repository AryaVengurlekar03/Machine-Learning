# FL-01 — Workflow Audit

**Author:** Arya Vengurlekar  
**Date:** 2026-07-27  
**Phase:** Setup

---

## Part 1 — Workflow Audit (Task Classification Table)

> Framework: Ethan Mollick's "On-boarding your AI Intern" — classify every
> recurring task as **Just Me**, **Delegate to AI (with review)**, **Collaborate
> with AI**, or **Fully Automate**.

| # | Task | Category | Classification | Rationale |
|---|------|----------|---------------|-----------|
| 1 | **Framing ML research questions** (choosing a project lane, writing hypotheses for the FlyRank internship) | Internship | **Just Me** | The research direction is a judgment call that requires my own understanding of the business problem; AI can't know what I actually want to investigate. |
| 2 | **Exploratory data analysis** (profiling columns, distribution checks, missing-value audits on the FlyRank dataset) | Internship | **Collaborate with AI** | AI is fast at generating pandas profiling code and suggesting checks, but I must interpret whether the patterns are real or artifacts. |
| 3 | **Writing and debugging Python data pipelines** (feature engineering, train/test splits, sklearn workflows) | Internship | **Collaborate with AI** | AI drafts boilerplate and catches syntax bugs quickly; I verify the logic, leakage safety, and whether outputs make domain sense. |
| 4 | **Reading ML papers and course material** (understanding new algorithms, statistical concepts) | Study | **Just Me** | Comprehension and building intuition cannot be outsourced — if I don't struggle with the material, I don't learn it. |
| 5 | **Writing capstone / assignment reports** (structuring claims, citing evidence, honest framing) | Internship | **Collaborate with AI** | AI helps with structure and phrasing, but every claim must come from my analysis; I review line-by-line to avoid over-stating results. |
| 6 | **Building side-project backends** (e.g., Binance Futures trading bot — API integration, order logic, error handling) | Side Project | **Collaborate with AI** | AI accelerates boilerplate (API wrappers, CLI scaffolding) but I must validate every trade-execution path — money is on the line. |
| 7 | **Debugging runtime errors** (tracebacks, dependency conflicts, environment issues) | All | **Delegate to AI (with review)** | Pasting a full traceback and letting AI diagnose is faster than manual Googling; I review the fix before applying it. |
| 8 | **Writing unit tests and validation scripts** | All | **Delegate to AI (with review)** | AI generates test skeletons and edge cases quickly; I review for coverage gaps and domain-specific assertions. |
| 9 | **Formatting and polishing markdown/documentation** (README files, data dictionaries, project docs) | All | **Delegate to AI (with review)** | Formatting is mechanical; AI handles tables, links, and consistent style well — I just verify accuracy of content. |
| 10 | **Networking and communication** (writing LinkedIn posts, emails to mentors/peers, internship updates) | Professional | **Just Me** | Authentic voice matters — AI-generated professional communication feels generic and risks misrepresenting my actual thoughts. |
| 11 | **Designing web front-ends** (HTML/CSS/JS for chatbot UIs, project demos) | Side Project | **Collaborate with AI** | AI generates responsive layouts and CSS fast; I direct the design vision and iterate on the result interactively. |
| 12 | **Git workflow** (branching, committing, resolving merge conflicts, keeping CI green) | All | **Fully Automate** | Commit message formatting and pre-commit checks can be templated; merge conflicts still need human judgment but are rare in solo repos. |
| 13 | **Reviewing and summarising long documentation** (API docs, library changelogs, data dictionaries) | Study | **Delegate to AI (with review)** | AI summarises accurately when given the full source text; I verify against the original before acting on the summary. |
| 14 | **Weekly planning and task prioritization** (deciding what to work on, estimating time) | Personal | **Just Me** | Only I know my energy levels, deadlines, and competing priorities — AI doesn't have that context. |

---

## Part 2 — Toolkit Setup Evidence

> **Action items (manual — cannot be done by AI):**

- [ ] **Claude account** — Sign up at [claude.ai](https://claude.ai) (free tier)
- [ ] **ChatGPT account** — Sign up at [chat.openai.com](https://chat.openai.com) (free tier)
- [ ] **Anthropic Academy** — Enroll in [AI Fluency: Framework & Foundations](https://academy.anthropic.com) and complete Module 1
- [ ] **Screenshot** of completed Module 1 → save as `work/screenshots/academy_module1.png`

---

## Part 3 — Claude Project Configuration

> **Action item (manual):** Create a Claude Project at [claude.ai/projects](https://claude.ai) with these custom instructions. Screenshot it → save as `work/screenshots/claude_project.png`.

### Suggested Custom Instructions (copy into your Claude Project)

```text
## Who I Am
I'm Arya Vengurlekar, an ML intern at FlyRank working on content-refresh
optimization. I'm also a CS student building side projects (trading bots,
web apps) to sharpen my full-stack and data skills.

## Tone Preferences
- Direct and concise — skip preamble, get to the point.
- Use code examples over prose when explaining technical concepts.
- Flag when you're uncertain instead of guessing confidently.
- Match my level: I know Python, pandas, sklearn, and basic stats —
  don't over-explain fundamentals, but do explain advanced concepts.

## Current Goals (July–August 2026)
1. Complete the FlyRank ML internship capstone (CTR/Engagement Opportunity
   Scoring lane) — honest claims, reproducible results.
2. Complete the AI Fluency course (FL-01 through FL-04).
3. Ship v1 of my Binance Futures trading bot with proper risk management.
4. Build portfolio-quality documentation for all projects.

## Working Rules
- Never fabricate data, citations, or results.
- When I paste an error, diagnose the root cause — don't guess.
- If a task requires my judgment (research direction, claim framing),
  say so instead of deciding for me.
```

---

## Part 4 — Three Target Tasks for FL-02 → FL-04

These are the three tasks I will reuse across the remaining AI Fluency assignments to build depth.

### Task 1: Exploratory Data Analysis (EDA) on the FlyRank Dataset

| Attribute | Definition |
|-----------|------------|
| **What** | Profile a new subset of the FlyRank dataset: distributions, missing values, correlations, and 3+ non-obvious insights documented with charts. |
| **Classification** | Collaborate with AI |
| **"Done Well" Means** | (1) Every chart has a title, axis labels, and a one-sentence interpretation. (2) At least one insight is something I didn't expect and can explain in my own words. (3) The notebook runs top-to-bottom with no errors (`Runtime → Run all`). (4) No data leakage — `trend_direction` and `trend_pct` never appear as features. |

### Task 2: Writing a Technical Report Section

| Attribute | Definition |
|-----------|------------|
| **What** | Draft a 400–600 word "Methodology" or "Results" section for the capstone report, with proper hedging language and evidence citations. |
| **Classification** | Collaborate with AI |
| **"Done Well" Means** | (1) Every claim maps to a specific table, chart, or metric in my notebook. (2) Language uses "observed / measured / directional" framing — no unsupported causal claims. (3) A peer could reproduce my result from the description alone. (4) I can explain every sentence if asked — nothing is copy-pasted without understanding. |

### Task 3: Debugging a Python Pipeline Error

| Attribute | Definition |
|-----------|------------|
| **What** | Take a real traceback from my ML pipeline or side project, diagnose the root cause, and implement a verified fix. |
| **Classification** | Delegate to AI (with review) |
| **"Done Well" Means** | (1) The root cause is identified, not just the symptom suppressed. (2) The fix is applied and the full pipeline/script runs without error. (3) I can explain *why* the error occurred and *why* the fix works. (4) If applicable, a guard (assertion, type check, or test) is added to prevent recurrence. |

---

## Submission Readiness Checklist

- [x] 14 tasks listed (≥ 10 required) — all from my actual week
- [x] Every task classified with one-line rationale
- [x] 3+ tasks marked "Just Me" with honest reasons (#1, #4, #10, #14)
- [x] 3 target tasks defined with measurable success criteria
- [ ] Tool accounts created and Academy enrollment evidenced (screenshots needed)
- [ ] Claude Project configured and screenshotted
