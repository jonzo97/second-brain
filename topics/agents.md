# AI Agents & Frameworks

Agent frameworks, orchestration tools, and agentic coding patterns.

## Frameworks

- [ ] [LangChain](https://docs.langchain.com/oss/python/langchain/overview) - LLM application framework
- [ ] [LangGraph](https://www.langchain.com/langgraph) - Stateful agent orchestration
- [ ] [Claude Agent SDK](https://docs.claude.com/en/api/agent-sdk/python) - Anthropic's agent SDK (Python)
- [ ] [OpenAI Agent Builder](https://platform.openai.com/agent-builder) - OpenAI's agent platform

## Open Source Agents

- [ ] [Goose](https://github.com/block/goose) - Open source AI agent (Block) - install, execute, edit, test with any LLM
- [ ] [DeerFlow](https://github.com/bytedance/deer-flow) - Deep Research framework (ByteDance) - web search, crawling, Python execution
- [ ] [Gemini Browser](https://github.com/browserbase/gemini-browser) - Gemini computer use on Browserbase
- [ ] [Letta](https://www.letta.com/blog/introducing-sonnet-4-5-and-the-memory-omni-tool-in-letta) - Memory omni-tool, persistent agent memory

## Research Topics

- [ ] Effort-based agent hierarchy — Opus 4.6 effort parameter: medium matches Sonnet 4.5 SWE-bench at 76% fewer tokens. Dynamic escalation patterns.
- [ ] Ralph fresh-context pattern — Spawn fresh Claude session per iteration, state via git only. Prevents context rot.
- [ ] Hook-driven agent triggering — PreToolUse/PostToolUse hooks for automatic agent spawning
- [ ] Trust scoring per agent — Track success/failure rates, adjust autonomy based on performance
- [ ] Cross-agent test verification — Independent verification agent validates test claims
- [ ] [DeerFlow deep research automation](https://github.com/bytedance/deer-flow) — Can it automate Gemini Deep Research handoff?
- [ ] Parallel worktree orchestration — L-thread/P-thread/B-thread taxonomy for multiple Ralph loops
