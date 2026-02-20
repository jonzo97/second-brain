# Claude Code Ecosystem

Skills, agents, plugins, hooks, commands, and extension repos for Claude Code.

## Official (Anthropic)

- [ ] [anthropics/skills](https://github.com/anthropics/skills) - Official Agent Skills repo (document skills, enterprise skills, skill spec + template)
- [ ] [Claude Code Plugins Docs](https://code.claude.com/docs/en/plugins) - Official plugin system documentation
- [ ] [Claude Code Hooks Guide](https://code.claude.com/docs/en/hooks-guide) - Official hooks documentation
- [ ] [Claude Agent SDK (Python)](https://docs.claude.com/en/api/agent-sdk/python) - Anthropic's agent SDK reference

## Awesome Lists & Directories

- [ ] [hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - The main community hub (~24k stars). Skills, hooks, commands, agents, CLAUDE.md files, alternative clients
- [ ] [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) - 300+ cross-platform agent skills (Claude Code, Codex, Gemini CLI, Cursor, etc.)
- [ ] [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents) - 100+ subagents across 10 categories (~10.8k stars)
- [ ] [ComposioHQ/awesome-claude-plugins](https://github.com/ComposioHQ/awesome-claude-plugins) - Curated plugins (commands, agents, hooks, MCP servers)
- [ ] [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) - Curated skills list
- [ ] [ccplugins/awesome-claude-code-plugins](https://github.com/ccplugins/awesome-claude-code-plugins) - Slash commands, subagents, MCP, hooks
- [ ] [davepoon/buildwithclaude](https://github.com/davepoon/buildwithclaude) - Aggregation hub: 117 agents, 175 commands, 28 hooks, 26 skills, 50 plugins (~2.5k stars)

## Agent & Skill Collections

- [ ] [wshobson/agents](https://github.com/wshobson/agents) - Production-ready: 112 agents, 146 skills, 16 orchestrators, 79 dev tools (~29k stars). Three-tier model strategy (Opus/Sonnet/Haiku)
- [ ] [wshobson/commands](https://github.com/wshobson/commands) - Companion slash commands repo
- [ ] [qdhenry/Claude-Command-Suite](https://github.com/qdhenry/Claude-Command-Suite) - 148 slash commands, 54 agents, 2 skills (~940 stars)
- [ ] [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) - 53 domain expert skills (marketing through engineering)
- [ ] [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) - Battle-tested configs from Anthropic hackathon winner

## Hooks

- [ ] [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) - Reference implementation for all 13 hook event types (~3.1k stars)
- [ ] [disler/claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) - Real-time monitoring/tracing for multi-agent workflows
- [ ] [karanb192/claude-code-hooks](https://github.com/karanb192/claude-code-hooks) - Copy-paste-ready hooks (safety, automation, notifications)
- [ ] [johnlindquist/claude-hooks](https://github.com/johnlindquist/claude-hooks) - TypeScript hook system with full type safety

## Build Frameworks

- [ ] [alirezarezvani/claude-code-skill-factory](https://github.com/alirezarezvani/claude-code-skill-factory) - Production toolkit for authoring skills, agents, hooks, commands at scale (~516 stars)
- [ ] [davila7/claude-code-templates](https://github.com/davila7/claude-code-templates) - CLI tool for configuring and monitoring Claude Code (~21k stars)
- [ ] [numman-ali/openskills](https://github.com/numman-ali/openskills) - `npm i -g openskills` - Universal skills loader, cross-platform

## Memory & Persistence

- [ ] [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) - Auto-captures session activity, compresses with AI, injects into future sessions (~29k stars)
- [ ] [memvid/claude-brain](https://github.com/memvid/claude-brain) - Single portable `.mv2` file memory. Rust core, sub-millisecond ops, git-committable

## Starter Kits & Examples

- [ ] [ChrisWiles/claude-code-showcase](https://github.com/ChrisWiles/claude-code-showcase) - Full example config (hooks, skills, agents, commands, GH Actions)
- [ ] [serpro69/claude-starter-kit](https://github.com/serpro69/claude-starter-kit) - Starter template with configs, skills, agents
- [ ] [lhohan/agent-chisels](https://github.com/lhohan/agent-chisels) - Reusable skills and commands

## HuggingFace

- [ ] [Agent Skills Generator (HF Space)](https://hf.co/spaces/Snaseem2026/agent-skills-generator) - Generate custom agent skills for Claude Code
- [ ] [Claude Code Slash Commands (HF Space)](https://hf.co/spaces/danielrosehill/Claude-Code-Slash-Commands) - Interactive slash command browser
- [ ] [ratanon/claude-code (HF Dataset)](https://hf.co/datasets/ratanon/claude-code) - Crawled Claude Code docs formatted for LLM training/RAG

## Notes

- The ecosystem is moving fast (2025-2026). Star counts may reflect hype as much as quality - check issue trackers
- "Skills" = model-invoked; "Agents" = subagents in `.claude/agents/`; "Commands" = user-invoked slash commands; "Hooks" = lifecycle event scripts
- Skills/agents/commands don't traverse parent dirs like CLAUDE.md does (known limitation)
