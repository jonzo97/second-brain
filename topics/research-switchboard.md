# Research Switchboard

Central hub for managing deep research prompts, ingesting results, and routing insights to the right projects. Second-brain owns the routing; cc_agents owns the research agent that does the squeezing.

## Status: Designing

---

## How It Works

```
┌─────────────────────────────────────────────────────────────┐
│                    RESEARCH SWITCHBOARD                       │
│                    (second-brain owns this)                   │
│                                                              │
│  1. QUEUE                                                    │
│     Prompts stored here ──→ User runs in Gemini Deep Research│
│                                                              │
│  2. INGEST                                                   │
│     Results saved to Google Drive ──→ Pull new docs          │
│     (auto-detect new files by name/date/format)              │
│                                                              │
│  3. SQUEEZE                                                  │
│     cc_agents research agent extracts insights               │
│     (uses deep-research-workflow.md pattern)                 │
│                                                              │
│  4. ROUTE                                                    │
│     Insights dispatched to destination projects              │
│     (routing table below)                                    │
└─────────────────────────────────────────────────────────────┘
```

---

## Prompt Queue

Prompts ready to copy-paste into Gemini Deep Research. Run 3 at a time.

Pre-written prompts also at `~/cc_agents/research/prompts/` (10 ready as of 2026-02-19).

### High Priority

| # | Topic | Prompt Location | Output Routes To | Status |
|---|-------|----------------|-----------------|--------|
| 01 | Deep research automation (DeerFlow, LangChain, browser) | `~/cc_agents/research/prompts/01_deep_research_automation.md` | cc_agents PRD or best practices | queued |
| 02 | Graph databases for agent feedback loops | `~/cc_agents/research/prompts/02_graph_databases.md` | cc_agents recipe + rag.md + learning.md | queued |
| 03 | Context estimator for Claude Code | `~/cc_agents/research/prompts/03_context_estimator.md` | cc_agents PRD | queued |
| 04 | RAG best practices 2026 | `~/cc_agents/research/prompts/04_rag_best_practices.md` | rag.md + NotebookLM podcast | queued |
| 05 | Cross-project delegation patterns | `~/cc_agents/research/prompts/05_cross_project_delegation.md` | cc_agents best practices + workflow-ideas.md | queued |

### Medium Priority

| # | Topic | Prompt Location | Output Routes To | Status |
|---|-------|----------------|-----------------|--------|
| 06 | Pre-compact context preservation | `~/cc_agents/research/prompts/06_pre_compact_preservation.md` | cc_agents best practices | queued |
| 07 | Obsidian as second-brain backend | `~/cc_agents/research/prompts/07_obsidian_evaluation.md` | NotebookLM podcast → mcp.md PRD | queued |
| 08 | NotebookLM integration patterns | `~/cc_agents/research/prompts/08_notebooklm_integration.md` | mcp.md + google-drive.md | queued |
| 09 | Effort parameter optimization | `~/cc_agents/research/prompts/09_effort_parameter.md` | cc_agents best practices | queued |
| 10 | Browser automation for research (Comet, Playwright) | `~/cc_agents/research/prompts/10_browser_automation.md` | cc_agents PRD if viable | queued |

### Future Prompts (To Write)

| Topic | Why | Routes To |
|-------|-----|-----------|
| Terminal/IDE setup for Claude Code on WSL | Daily pain point, need to pick a terminal | dev-tools.md |
| GitHub Copilot token leverage patterns | Maximize corporate free tokens | workflow-ideas.md |
| Claude Co-Work capabilities & limits | High priority research, may replace meta-project | learning.md + workflow-ideas.md |
| Graph-db for personal knowledge management | Connects to RAG, Obsidian, cross-project memory | learning.md + rag.md |
| Inter-project agent communication patterns | Formalize cross-project mailbox | workflow-ideas.md + cc_agents |

---

## Routing Table

Where squeezed insights go based on content type:

| Content Type | Destination | Example |
|-------------|-------------|---------|
| **Actionable implementation spec** | `~/cc_agents/pipeline/` as PRD | "Build a RAG pipeline with ChromaDB" |
| **Best practices / reference** | `~/cc_agents/docs/` | "Agent orchestration patterns" |
| **Learning / broad understanding** | NotebookLM podcast → Google Drive | "How graph databases work" |
| **Tool/repo discovery** | `second-brain/topics/*.md` | "New RAG tool found: rag-cli" |
| **Architecture decision** | `second-brain/topics/*.md` or ADR | "Obsidian vs alternatives evaluation" |
| **FPGA-specific** | `~/fpga_projects/` (TBD) | "AI inference on PolarFire SoC" |
| **Cross-project pattern** | `~/.claude/cross-project.md` mailbox | "New delegation protocol" |

---

## Google Drive Connection (CRITICAL DEPENDENCY)

**Status**: Not configured yet. This is the bottleneck for the whole pipeline.

### The Problem
Research outputs are saved manually to Google Drive after running Gemini Deep Research. Need automated pull into the ingestion pipeline.

### Connection Options to Research

| Approach | Pros | Cons | Effort |
|----------|------|------|--------|
| **Google Drive MCP Server** | Native Claude Code integration, read/write/search | Need to find/build one, auth setup | Medium |
| **Google Drive API (Python)** | Full control, well-documented, OAuth2 | More code to write, token refresh | Medium |
| **Google Drive API via cc_agents recipe** | Reusable pattern, fits existing architecture | Need to build recipe first | Medium |
| **rclone CLI** | Simple mount/sync, no code needed | Less granular control, not MCP-integrated | Low |
| **gdrive CLI** | Lightweight, scriptable | Less maintained, auth can be finicky | Low |

### Research Tasks
- [ ] Search for existing Google Drive MCP servers (community or official)
- [ ] Check if Gemini Deep Research can export directly to a specific Drive folder
- [ ] Evaluate rclone vs API vs MCP for this use case
- [ ] Design the auth flow (OAuth2, service account, or API key?)
- [ ] Security: what data is safe to pull through? (No MCHP proprietary content)

### Ideal Drive Folder Structure
```
Google Drive/
└── AI Research/
    ├── pending/          ← Gemini outputs land here
    ├── ingested/         ← Moved here after processing
    └── archive/          ← Old research, kept for reference
```

---

## Ingestion Tracking System

Track which files have been processed to avoid re-ingestion and detect new arrivals.

### File Detection Pattern
```
Look for files matching:
  - Location: Google Drive / AI Research / pending/
  - Format: .md, .pdf, .docx, .txt (Gemini exports)
  - Name pattern: *deep_research*, *gemini*, or prompt number prefix
  - Date: after last ingestion timestamp
```

### Tracking File: `.research-tracker.json`
```json
{
  "last_scan": "2026-02-19T00:00:00Z",
  "ingested": [
    {
      "file": "01_deep_research_automation_output.md",
      "ingested_at": "2026-02-19T12:00:00Z",
      "routed_to": ["cc_agents/docs/deep-research-best-practices.md"],
      "prompt_id": "01",
      "status": "routed"
    }
  ],
  "pending": []
}
```

### States
```
new → detected → ingesting → squeezed → routed → archived
```

---

## Session Start Hook (Auto-Ingestion)

**Idea**: On session start in second-brain, automatically check for new research outputs and launch the ingestion agent in the background.

### Concept
```bash
# .claude/hooks/SessionStart — research ingestion check
# 1. Check Google Drive for new files in pending/
# 2. If new files found, notify user and optionally launch cc_agents research agent
# 3. Update .research-tracker.json
```

### Implementation Steps (Future)
- [ ] Get Google Drive connection working first (blocker)
- [ ] Write a lightweight scan script (check pending/ folder, compare to tracker)
- [ ] Integrate as SessionStart hook or background agent on session open
- [ ] Research agent (cc_agents) does the heavy lifting: squeeze → route → update tracker
- [ ] Consider: should the agent auto-run or just notify? (ADHD: notification is better — "You have 3 new research outputs to process")

### Alternative: Manual Trigger
If auto-run feels too aggressive, a Claude Code skill `/ingest-research` could:
1. Scan Drive for new outputs
2. Show what's new
3. Let user pick which to process
4. Launch squeeze + route for selected items

---

## Pain Points & Open Questions

- **No API keys with consumer Gemini subscription** — Gemini Deep Research is manual (run in browser, save to Drive). Can't fully automate the "run" step yet.
- **Gemini export to .md is broken** — Workaround: Save to Google Docs → pull from Drive as .docx or plain text
- **How does cc_agents research agent get invoked from here?** — Cross-project mailbox? Direct `claude -p` call? Shared MCP?
- **Should second-brain own the tracker or should it live in cc_agents?** — Leaning second-brain since this is the switchboard
- **What if a research output routes to multiple destinations?** — Squeeze once, copy relevant sections to each destination
