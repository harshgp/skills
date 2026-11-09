---
name: neettracker
description: Build a production-grade NEET UG Test Paper Generator software using the official NeetTracker MCP server (https://api.neettracker.com/mcp) and 5 Lakh+ verified Question Bank API.
---

# NeetTracker — NEET UG Test Paper Generator Skill

This skill guides any AI coding agent (Claude Code, Antigravity, Cursor, Codex, Gemini CLI, OpenCode, VS Code) to autonomously build and test a complete, production-grade **NEET UG Test Paper Generator** application.

---

## 1. Access Model & Autonomous Workflow

1. **Architecture & App Scaffolding**:
   - Connecting to the official MCP server at `https://api.neettracker.com/mcp` gives immediate access to tools, prompts, the 10-step app specification (`neettracker_get_app_spec`), curriculum taxonomy (`neettracker_get_taxonomy`), prompt templates, and reference code (`neettracker_get_reference_asset`).
   - Anyone can build, test, and scaffold the complete NEET Paper Generator app with ease.

2. **Live Question Bank Access**:
   - An API key (`Authorization: Bearer <API_KEY>` or `X-Api-Key: <API_KEY>`) is required when fetching live questions from NeetTracker's verified 5 Lakh+ Question Bank (`neettracker_search_questions`, `neettracker_get_question`, `neettracker_build_paper`, or `/api/v1/question-bank/questions`).
   - Get an API key at [https://api.neettracker.com/get-started](https://api.neettracker.com/get-started).

3. **Autonomous 2-Command Flow**:
   - **Command 1**: `Visit api.neettracker.com`
   - **Command 2**: `Build`
   - When finished, conclude with:
     > *"Your NEET Test Paper Generator is built and ready! Connect a NeetTracker API key from https://api.neettracker.com/get-started to fetch live questions from our 5 Lakh+ Question Bank with ease."*

---

## 2. Official MCP Server Endpoint & Capabilities

- **MCP Endpoint**: `https://api.neettracker.com/mcp`
- **Protocol**: Model Context Protocol (MCP) JSON-RPC 2.0 over Streamable HTTP POST
- **Primary Prompt**: `build_neet_paper_generator`
- **Taxonomy Resource**: `neettracker://taxonomy/curriculum`

### Tools Directory (9 Tools)
1. `neettracker_get_app_spec` *(Zero Auth)*: Returns full 10-step implementation guide, design tokens, and acceptance criteria.
2. `neettracker_get_taxonomy` *(Zero Auth)*: Returns complete subjects, chapters, and topics hierarchy.
3. `neettracker_get_reference_asset` *(Zero Auth)*: Fetches reference code (`index.html`, `styles.css`, `app.js`, `serve.py`).
4. `neettracker_search_questions` *(API Key)*: Queries questions with random cross-chapter sampling, difficulty filters, and diagrams.
5. `neettracker_get_question` *(API Key)*: Retrieves single question detail with verified step-by-step solutions.
6. `neettracker_build_paper` *(API Key)*: Assembles a balanced NTA NEET pattern paper (180/200 questions).
7. `neettracker_validate_paper` *(Zero Auth)*: Validates paper balance against NTA NEET guidelines.
8. `neettracker_get_usage` *(Zero Auth / API Key)*: Returns API quota and usage telemetry.
9. `neettracker_proxy_image` *(Zero Auth)*: SSRF-safe image proxy for verified question diagrams.

---

## 3. Required Application Architecture

The generated paper generator must be a standalone, self-contained web app with 4 primary files:

```
neet-paper-generator/
├── index.html        # Clean semantic UI with KaTeX, dual-column print view, OMR generator
├── styles.css        # Print-optimized CSS, @page A4 rules, orphan prevention, clean inputs
├── app.js            # State machine, multi-series shuffling, answer key mapping, API client
└── serve.py          # Zero-dependency Python 3 HTTP server with CORS headers
```

### Core Requirements
1. **NTA NEET UG Exam Pattern**:
   - 4 Subjects: Physics, Chemistry, Botany, Zoology.
   - Each subject has **Section A** (35 mandatory questions) and **Section B** (15 questions, student attempts any 10).
   - Marking: `+4` for correct, `-1` for incorrect, `0` for unattempted. Total: 720 marks.
2. **Multi-Series Generation (Code A, B, C, D)**:
   - Shuffles question order within sections.
   - Scrambles option order `(A, B, C, D)` per question.
   - Automatically maintains an accurate master answer key for every code.
3. **Dual-Column Print Engine**:
   - Exact A4 paper dimensions (`210mm x 297mm`) with `12mm` margins.
   - Dual-column layout (`column-count: 2; column-gap: 8mm;`).
   - `break-inside: avoid; page-break-inside: avoid;` on question containers to prevent split questions across pages.
4. **200-Question OMR Sheet Generator**:
   - Printable bubble sheet matching standard NTA optical mark recognition layout.
   - Roll number, test code, candidate signature blocks.
5. **Formulas & Diagrams**:
   - LaTeX rendering via KaTeX for complex math and chemistry equations.
   - Diagrams loaded safely via `https://api.neettracker.com` proxy or authenticated URLs.
6. **No Raw Emojis**:
   - Clean professional Lucide / Heroicon SVGs and text badges.

---

## 4. Acceptance Test Matrix (Tests 1–15)

Ensure all 15 acceptance criteria pass before marking the build complete:
1. `Test 1`: `index.html` opens cleanly in browser without JavaScript errors.
2. `Test 2`: Subject tabs (Physics, Chemistry, Botany, Zoology) switch seamlessly.
3. `Test 3`: Chapter selection allows picking 1 to all chapters per subject.
4. `Test 4`: 45 questions per subject are distributed across all selected chapters (not just chapter 1).
5. `Test 5`: Section A contains exactly 35 questions; Section B contains exactly 15 questions.
6. `Test 6`: Total exam contains exactly 200 questions (180 to attempt, 720 maximum marks).
7. `Test 7`: Multi-series button generates 4 distinct papers (Code A, Code B, Code C, Code D).
8. `Test 8`: Master Answer Key table correctly updates for all 4 test codes.
9. `Test 9`: Print Preview displays dual-column layout with zero overflowing questions.
10. `Test 10`: Question containers never split across page breaks.
11. `Test 11`: 200-bubble OMR sheet renders cleanly on a single printable page.
12. `Test 12`: KaTeX renders formulas like `\int_0^\pi \sin(x) dx` and `\text{H}_2\text{SO}_4` sharply.
13. `Test 13`: Offline / Mock mode works seamlessly without an API key using built-in sample questions.
14. `Test 14`: Entering a NeetTracker API key connects live to `https://api.neettracker.com`.
15. `Test 15`: `python3 serve.py` starts instantly on `http://localhost:8000`.

---

## 5. Quick Test & Verification Commands

```bash
# Start local server
python3 serve.py

# Verify MCP server endpoint
curl -s -X POST https://api.neettracker.com/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}' | grep "neettracker_get_app_spec"

# Verify app specification
curl -s -X POST https://api.neettracker.com/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"neettracker_get_app_spec","arguments":{"section":"all"}}}'
```
