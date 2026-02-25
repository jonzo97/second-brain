# AI Agents & Frameworks

Agent frameworks, orchestration tools, and agentic coding patterns.

## Frameworks

- [ ] [LangChain](https://docs.langchain.com/oss/python/langchain/overview) - LLM application framework
- [ ] [LangGraph](https://www.langchain.com/langgraph) - Stateful agent orchestration
- [ ] [Claude Agent SDK](https://docs.claude.com/en/api/agent-sdk/python) - Anthropic's agent SDK (Python)
- [ ] [OpenAI Agent Builder](https://platform.openai.com/agent-builder) - OpenAI's agent platform

## Open Source Agents

- [ ] [Goose](https://github.com/block/goose) - Open source AI agent (Block) - install, execute, edit, test with any LLM
- [ ] [DeerFlow 2.0](https://github.com/bytedance/deer-flow) - Deep Research framework (ByteDance) - multi-agent hierarchy (Coordinator/Planner/Researcher/Coder/Reporter), LangGraph state machine, model-agnostic via LiteLLM, extensible "Skills" system. **v2.0 is a "super agent harness"** -- potential self-hosted replacement for Gemini Deep Research.
- [ ] [Gemini Browser](https://github.com/browserbase/gemini-browser) - Gemini computer use on Browserbase
- [ ] [Letta](https://www.letta.com/blog/introducing-sonnet-4-5-and-the-memory-omni-tool-in-letta) - Memory omni-tool, persistent agent memory
- [ ] [GPT Researcher](https://github.com/UberGuidoZ/GPT-Researcher) - Autonomous multi-source research agent. Scrapes 20+ sites per query, parallel crawlers, supports Ollama + DuckDuckGo for zero-cost local research. (from research #01)
- [ ] [Stanford STORM](https://github.com/stanford-oval/storm) - Perspective-guided article synthesis. Simulates conversations between writer and topic experts. Supports local PDF research via VectorRM. (from research #01)
- [ ] [II-Researcher](https://github.com/Intelligent-Internet/ii-researcher) - Modular research framework using LiteLLM + BAML. Separates "Reasoning" models (R1) for analysis and "Fast" models for compression. (from research #01)
- [ ] [browser-use](https://github.com/browser-use/browser-use) - Semantic browser automation via LLM. Uses DOM/accessibility tree instead of brittle CSS selectors. Can be deployed as MCP server. (from research #01)
- [ ] [mcp-browser-use](https://github.com/Saik0s/mcp-browser-use) - MCP server wrapping browser-use for Claude Code. HTTP transport (survives long tasks). (from research #01)
- [ ] [notebooklm-kit](https://github.com/photon-hq/notebooklm-kit) - TypeScript SDK for programmatic NotebookLM access. Batch upload sources from URLs, files, YouTube. (from research #01)

## Research Topics

- [ ] Effort-based agent hierarchy — Opus 4.6 effort parameter: medium matches Sonnet 4.5 SWE-bench at 76% fewer tokens. Dynamic escalation patterns.
- [ ] Ralph fresh-context pattern — Spawn fresh Claude session per iteration, state via git only. Prevents context rot.
- [ ] Hook-driven agent triggering — PreToolUse/PostToolUse hooks for automatic agent spawning
- [ ] Trust scoring per agent — Track success/failure rates, adjust autonomy based on performance
- [ ] Cross-agent test verification — Independent verification agent validates test claims
- [x] [DeerFlow deep research automation](https://github.com/bytedance/deer-flow) — ANSWERED (research #01): DeerFlow 2.0 is a self-hosted research OS, not a Gemini automation layer. It replaces Gemini DR rather than wrapping it. See `cc_agents/docs/research-automation-best-practices.md`.
- [ ] Parallel worktree orchestration — L-thread/P-thread/B-thread taxonomy for multiple Ralph loops

## Context & Memory Tools
*Added from research squeezes (2026-02-22)*

- [ ] [Tree-sitter](https://tree-sitter.github.io/tree-sitter/) — Language-agnostic AST parser. Used by Aider for Repo Maps — generates structural code graphs (who-calls-whom, type hierarchies) that vector embeddings miss. (from research: agentic context mgmt)
- [ ] [Aider repomap](https://github.com/paul-gauthier/aider) — Study `repomap.py` for AST-based context construction. Uses Tree-sitter + PageRank to build compressed graph of definitions ranked by structural importance. (from research: agentic context mgmt)
- [ ] [memory-bank-mcp-server](https://github.com/memory-bank-mcp-server) — MCP server exposing Memory Bank as a resource. Future: allows memory decoupling from filesystem, cross-agent sharing. (from research: agentic context mgmt)
- [ ] [Cline Memory Bank](https://docs.cline.bot/prompting/cline-memory-bank) — Reference implementation of File-Centric Memory pattern. Active community, validated by research as recommended archetype. (from research: agentic context mgmt)
- [ ] `ccusage` — Lightweight status line integration for Claude Code. Handles native JSON pipe, ANSI color output, threshold flags. `npm install -g ccusage` (from research: CC context mgmt)
- [ ] `claude-code-usage-monitor` (cmonitor) — Live dashboard with predictive analytics. Shows tokens remaining before degradation. (from research: CC context mgmt)
- [ ] `ClaudeCTX` — Profile switcher for toggling between API (1M) and Pro (200K) context configurations. (from research: CC context mgmt)
- [ ] [inotify-tools](https://github.com/inotify-tools/inotify-tools) — Interrupt-driven filesystem watching for WSL2 mailbox sync. `sudo apt install inotify-tools` (from research: cross-project coordination)
- [ ] [Context7](https://context7.com/) — MCP server providing version-specific library docs to agents without manual copy-paste. Evaluate for cc_agents. (from research: cross-project coordination)
- [ ] Agent Watch — Git hook-based tool that discovers active chat sessions across Claude Code/Cursor/Copilot, merges learned patterns into CLAUDE.md files. Pattern to replicate. (from research: cross-project coordination)
- [ ] [roo-code-memory-bank](https://github.com/GreatScottyMac/roo-code-memory-bank) — Reference implementation of Memory Bank pattern for Roo Code/Cline. Study for pattern extraction. (from research: cross-project coordination)
- [ ] [Supermemory MCP](https://github.com/supermemory) — Cross-client context sharing via MCP. Evaluate if flat mailbox becomes bottleneck. (from research: cross-project coordination)

## Framework Analysis (5-Repo Survey, Feb 2026)
*Source: cc_agents analysis of 5 major agent frameworks*

### Frameworks Analyzed
- [ ] **BMAD-METHOD** — Adversarial two-pass review (cynical→professional), `critical_actions` behavioral constraints, story-file handoff pattern
- [ ] **GSD** — Wave-based parallel execution, PLAN.md-as-executable-prompt, `files_to_read` bootstrap (pass paths not content), goal-backward verification (`must_haves`)
- [ ] **spec-kit** (GitHub) — Constitution pattern (versioned project governance), spec→plan→tasks pipeline, `analyze` command (read-only consistency audit)
- [ ] **wshobson/agents** — `model:inherit` tier (user controls cost), progressive skill loading, file ownership for parallel builders
- [ ] **claude-task-master** — PRD→tasks pipeline with topological sort, `testStrategy` per task, `findNextTask` algorithm

### Three Convergent Patterns (all 5 frameworks agree)
1. **Plans as first-class file artifacts** — not conversation context
2. **Verification against reality, not claims** — don't trust summaries
3. **Explicit behavioral constraints** — NEVER/ALWAYS rules beat positive guidance

Full analysis at `~/cc_agents/research/active/agent-frameworks-analysis.md`.

## cc_agents Cross-References

Recipes and patterns living in `~/cc_agents/` that are relevant here:
- `~/cc_agents/recipes/chromadb.md` — Direct-code ChromaDB recipe (skip MCP, use Python)
- `~/cc_agents/docs/deep-research-workflow.md` — Repeatable research cycle (prompt→ingest→squeeze→PRD→execute)
- `~/cc_agents/docs/context-management-best-practices.md` — Context management constraints, patterns, anti-patterns (from research squeezes)
- `~/cc_agents/docs/cross-project-patterns.md` — Cross-project coordination patterns and protocols
- `~/cc_agents/recipes/_PATTERN.md` — Template for direct-code recipes
- `~/cc_agents/research/prompts/` — 10 pre-written Gemini Deep Research prompts ready to batch-run
