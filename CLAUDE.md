# second-brain — Project Instructions

## What This Is
Personal knowledge base and "second brain" — curated tools, repos, articles, research topics, and project ideas. Imported from Chrome bookmarks and expanded over time. Will eventually integrate with OpenClaw.

## Structure
- `bookmarks/` — Raw bookmark exports and structured data
- `topics/` — Organized by topic area (see README.md for index)

## Cross-Project Communication

This project is part of a multi-project workspace. A shared mailbox exists for coordination:

**Shared mailbox:** `~/.claude/cross-project.md`
- Automatically checked on session start via inbox hook (shows pending messages)
- If user says **"check your inbox"** mid-session, read `~/.claude/cross-project.md` for pending messages
- After reading a message, update its status: `pending` → `read by second-brain (YYYY-MM-DD)`
- After acting on it: `read` → `completed by second-brain (YYYY-MM-DD)`
- Write handoff notes here when your work produces artifacts useful to other projects
- See `~/cc_agents/docs/cross-project-patterns.md` for the full pattern documentation

### Sibling Projects
| Project | Path | What's There |
|---------|------|-------------|
| **cc_agents** | `~/cc_agents/` | Agent definitions, orchestration patterns, recipes |
| cc_agents recipes | `~/cc_agents/recipes/` | Direct-code patterns for tools (Playwright, ChromaDB, jq, HTTP, SQLite) — use instead of MCP when possible |
| cc_agents docs | `~/cc_agents/docs/` | Orchestrator guide, tool catalog, deep research workflow, cross-project patterns |

### Deep Research Workflow
When researching a new topic deeply, follow the workflow at `~/cc_agents/docs/deep-research-workflow.md`:
1. Generate a structured prompt for Gemini Deep Research
2. User runs it manually in Gemini
3. Ingest the output, squeeze out actionable insights
4. Generate a PRD if building something
5. Archive the cycle

### Agents Available
Global agents are deployed at `~/.claude/agents/` (scout, research, planner, builder, reviewer). Use them via the Task tool with team presets when tasks are complex enough to warrant multi-agent orchestration. See `~/cc_agents/teams/` for preset configurations.

## Working With Topics
- Each topic file is a curated collection of links, tools, and notes
- When adding new items, categorize into existing topics or create new ones
- Keep the README.md topic index updated
- Mark items as explored/reviewed when you've evaluated them
