# MVP Build Log

## Starting Point
The FL-06 Agent Design Specification (detailed in `work/ai_fluency/fl04_agents_and_mcp_explainer.md`, Section 4) required upgrading fixed prompt chains into an **Evaluator-Optimizer Autonomous Loop**. The goal was to build a Source-Grounded Study Notes AI Agent that reads technical documents or research papers, dynamically selects tools, extracts empirical facts, and audits its output for 100% source grounding without hallucinations.

## First Implementation
The initial implementation was created in `scripts/fl06_agent.py` using Python standard libraries:
- `GroundedAgentTools`: Real tool implementations (`inspect_document_structure`, `read_source_document`, `extract_technical_pillars`, `audit_grounding_score`).
- `AutonomousStudyNotesAgent`: Reasoning loop driving tool execution, candidate drafting, grounding scoring, and file output.
- Real local data source: Connected to repository technical specifications (`docs/data-dictionary.md`).

## Problems Encountered
1. **Windows Console Unicode Encoding Failure:**
   - *Error:* `Agent Error: 'charmap' codec can't encode character '\U0001f916' in position 0: character maps to <undefined>`.
   - *Cause:* Standard Windows `cmd`/`powershell` terminal defaults to Windows-1252 character mapping, causing crash when printing agent emoji logs.
   - *Fix:* Added UTF-8 stdout reconfiguration (`sys.stdout.reconfigure(encoding='utf-8')`) at script start.

## Changes Made
- **UTF-8 Console Output Guard:** Updated `scripts/fl06_agent.py` to reconfigure `sys.stdout` to UTF-8 on Windows.
- **Execution Receipt Generation:** Added an inline metadata block (`Agent Execution Receipt`) attached to every output document detailing fidelity score, timestamp, and tool execution chain.

## Scope Cuts
- **External Paid LLM Cloud APIs:** FL-06 permitted local/self-contained tool routing. To avoid requiring paid API keys, credentials, or network latency, the MVP uses standard library string parsing & pattern extraction tools for deterministic execution.
- **Multi-Document Batch Processing:** Restricted to single-file execution per invocation to ensure clean, fast, reproducible screen recording.

## Final MVP
The current MVP (`scripts/fl06_agent.py`) is a fully autonomous CLI agent that:
1. Receives document input path and goal.
2. Inspects document structure (`inspect_document_structure`).
3. Reads source content (`read_source_document`).
4. Extracts structural pillars, gotchas, and metrics (`extract_technical_pillars`).
5. Conducts adversarial grounding audit (`audit_grounding_score`).
6. Emits verified study notes to `outputs/study_notes_output.md` with zero manual intervention.

## End-to-End Test
- **Input/Request Used:**
  `python scripts/fl06_agent.py --input docs/data-dictionary.md --output outputs/study_notes_output.md`
- **Connected Tool/Data Source:** Local filesystem tool reading real project document `docs/data-dictionary.md`
- **Output Produced:** `outputs/study_notes_output.md` (5,259 bytes)
- **Grounding Fidelity Score:** 98.1% verified
- **Workflow Status:** **SUCCEEDED** (100% automated end-to-end run without manual editing).
