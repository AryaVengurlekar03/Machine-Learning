# FL-04 Explainer: Workflows, Autonomous Agents, and MCP

**Author:** Arya Vengurlekar  
**Course:** AI Fluency — Build (core)  
**Date:** March 2026  

---

## 1. Workflows vs. Agents: The Core Distinction

In modern AI engineering, "agent" is often used loosely to describe any system using a Large Language Model. As Anthropic explains in *Building Effective Agents*, there is a fundamental distinction between a **workflow** and an **agent**.

### What is a Workflow?
A **workflow** is a system where the control flow—the sequence of steps, branches, loops, and tools—is programmatically fixed by human code or pre-defined prompt chains. The LLM performs text generation or extraction at specific nodes, but it does not decide *which* step happens next. Common workflow patterns include:
* **Prompt Chaining:** Sequential execution where Output A becomes Input B.
* **Routing:** Directing inputs down fixed decision paths using classification rules.
* **Parallelization:** Running multiple LLM prompts concurrently and aggregating outputs.

### What is an Agent?
An **agent** is a system where the LLM dynamically directs its own control flow. Given a high-level goal, the model autonomously plans actions, selects which external tools to call, evaluates tool outputs, and decides whether to take another action or stop. The loop is driven by the model's own reasoning rather than a hardcoded script.

```text
WORKFLOW: [Step 1: Gather] ──► [Step 2: Synthesize] ──► [Step 3: Draft] ──► [Step 4: Review]
 (Fixed control flow determined by developer code/prompts)

AGENT:    Goal ──► [LLM Reasoner] ──► Select Tool ──► Evaluate Result ──► Loop / Stop
 (Dynamic control flow determined autonomously by the LLM)
```

---

## 2. Model Context Protocol (MCP) & Its Three Primitives

Connecting every AI model to every external tool creates an unsustainable integration problem. The **Model Context Protocol (MCP)** is an open standard—often described as the "USB-C port for AI"—that standardizes how models connect to local filesystems, databases, APIs, and tools.

MCP defines three core primitives:
1. **Tools:** Executable functions exposed by the MCP server that the model can invoke to act or fetch dynamic data (e.g., `read_file`, `execute_sql`).
2. **Resources:** Read-only data sources attached to the model as context (e.g., log files, database schemas, local documents).
3. **Prompts:** Standardized, reusable prompt templates managed by the MCP server that users or applications can invoke with arguments.

By decoupling tool implementation from model logic, MCP enables clients like Claude to safely interact with local repositories and live services.

---

## 3. Classification of the FL-04 Research Pipeline

In Week 5, I built a 4-step **Source-Grounded Study Notes Pipeline** (FL-04) that processes research papers through four sequential prompts:
1. **Step 1: Gather** (Extract raw facts and metrics)
2. **Step 2: Synthesize** (Organize into thematic pillars)
3. **Step 3: Draft** (Generate Markdown study notes)
4. **Step 4: Review** (Adversarial grounding audit against source text)

### Verdict: WORKFLOW (Prompt Chain)

My FL-04 pipeline is strictly a **Workflow**, not an agent. The control flow is 100% hardcoded. Step 1 feeds Step 2, Step 2 feeds Step 3, and Step 3 feeds Step 4. The LLM cannot decide to skip a step, loop back, or search for missing context. Regardless of paper complexity, it executes the identical 4-step chain.

---

## 4. Upgrading FL-04 to an Autonomous Agent

To upgrade FL-04 into an **Autonomous Agent**, we must replace the fixed prompt chain with an **Evaluator-Optimizer Autonomous Loop**.

### Concrete Agent Upgrade Architecture:
1. **Goal:** *"Produce comprehensive, 100% source-grounded study notes for this paper."*
2. **MCP Tool Suite:** `inspect_pdf_structure`, `read_page_range`, `extract_table_data`, and `evaluate_grounding_score`.
3. **Dynamic Execution Loop:**
   * The agent first calls `inspect_pdf_structure` to assess paper length and layout.
   * If pages 12–15 contain dense ML tables, the agent autonomously decides to call `extract_table_data(15)`.
   * After drafting notes, the agent runs `evaluate_grounding_score`. If the score reveals missing sample sizes or metric errors, the agent autonomously loops back, re-queries the PDF via MCP tools, fixes the error, and re-evaluates until quality threshold is met.

---

## 5. Working Connector Evidence (Three Tool Tasks)

Below is evidence of three tasks executed via system and file connectors that plain chat alone could not perform without environment access.

### Task 1: Reading Local Code (`view_file`)
* **Goal:** Inspect local Python notebook script `scripts/build_w02_notebook.py`.
* **Tool Invoked:** `view_file`
* **Arguments:** `{"AbsolutePath": ".../scripts/build_w02_notebook.py", "StartLine": 1, "EndLine": 20}`
* **Output Snippet:**
  ```python
  1: import json
  2: import io
  3: import pandas as pd
  ...
  15: def execute_cell(code_str, execution_count):
  ```

### Task 2: Searching Local Docs (`grep_search`)
* **Goal:** Search repository markdown docs for data contracts.
* **Tool Invoked:** `grep_search`
* **Arguments:** `{"Query": "contract", "SearchPath": ".../docs", "Includes": ["*.md"]}`
* **Output Snippet:**
  ```json
  {"File": "c:\\...\\docs\\ml-intern-dataset-and-lane-guide.md"}
  ```

### Task 3: Auditing Repo Rules (`view_file`)
* **Goal:** Inspect repository configuration file `AGENTS.md`.
* **Tool Invoked:** `view_file`
* **Arguments:** `{"AbsolutePath": ".../AGENTS.md"}`
* **Output Snippet:**
  ```markdown
  1: # Agent instructions
  2: Before any task in this repo: read `skills/README.md` — it is the router.
  ```
