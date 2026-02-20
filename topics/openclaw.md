# OpenClaw

Personal AI assistant platform. #1 trending on GitHub (Feb 2026). This is the eventual integration target for this second-brain repo.

## Overview

- **What**: Open-source, local-first autonomous AI agent that runs persistently on your machine
- **Creator**: Peter Steinberger (Austrian dev, joined OpenAI Feb 15, 2026)
- **Repo**: [openclaw/openclaw](https://github.com/openclaw/openclaw) - 212K stars
- **Install**: `npm install openclaw`
- **License**: Open source, transitioning to independent foundation (backed by OpenAI)
- **History**: Originally "Clawdbot" -> "Moltbot" (Anthropic legal threat over name) -> "OpenClaw"

## Architecture

- **Gateway**: WebSocket RPC on `127.0.0.1:18789` (Node.js 22+), single gateway per host
- **Channel Adapters**: WhatsApp (Baileys), Telegram (grammY), Discord (discord.js), 50+ platforms
- **Agent Runtime**: Assembles context, calls LLM, executes tools
- **Plugin System**: Extends channels, memory, tools, LLM providers
- **State**: `~/.openclaw/` - JSON5 config, append-only logs, SQLite with vector embeddings
- **LLM Backends**: Pluggable - Claude, GPT, Gemini, local models. Multi-agent routing per channel

## Key Integrations

### Obsidian (First-class)
- [ ] Read/write Obsidian vaults directly
- [ ] Store OpenClaw workspace inside vault (`~/obsidian-vault/openclaw`)
- [ ] Automated daily notes, health data ingestion, calendar aggregation
- [ ] Proactive: agent checks things in background and surfaces what you need
- [ ] [Official Obsidian skill](https://github.com/openclaw/openclaw/tree/main/skills/obsidian)

### Messaging (50+)
WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Teams, Matrix, and more. Voice notes supported.

### Other
- [ ] Notion sync also available
- [ ] Home automation
- [ ] Email management
- [ ] Web browsing

## Skills & ClawHub

- **Skills**: Markdown-based guides (`skills/<skill>/SKILL.md`) that teach the agent capabilities
- **ClawHub**: [clawhub.ai](https://claw-hub.net/) - Public skill registry, 3,000+ skills, vector search
- **Repo**: [openclaw/clawhub](https://github.com/openclaw/clawhub)

## Security Concerns (Important!)

- **ClawHavoc attack**: 1,184 malicious skills compromised ClawHub
- **Credential leaks**: Snyk found 7.1% of skills (283 of ~3,984) exposed API keys, credit card numbers, PII
- **Supply chain risk**: Skills pass through LLM context window, so data can leak
- **Mitigations**: Loopback binding, device pairing, Docker sandboxing, token auth
- **SecureClaw**: Open-source security tool debuted in response
- **Enterprise**: Netzilo AI Edge announced governance layer (Feb 19, 2026)

**Bottom line**: Vet every skill before installing. Don't install skills that touch sensitive data without review.

## Hardware

- [ ] Runs on Raspberry Pi - [official guide](https://www.raspberrypi.com/news/turn-your-raspberry-pi-into-an-ai-agent-with-openclaw/)

## Reading

- [ ] [Fortune profile of Peter Steinberger](https://fortune.com/2026/02/19/openclaw-who-is-peter-steinberger-openai-sam-altman-anthropic-moltbook/)
- [ ] [TechCrunch - Steinberger joins OpenAI](https://techcrunch.com/2026/02/15/openclaw-creator-peter-steinberger-joins-openai/)
- [ ] [Architecture deep dive (Substack)](https://ppaolo.substack.com/p/openclaw-system-architecture-overview)
- [ ] [Obsidian second brain integration](https://notesbylex.com/openclaw-the-missing-piece-for-obsidians-second-brain)
- [ ] [Snyk security research](https://snyk.io/blog/openclaw-skills-credential-leaks-research/)

## Integration Plan (Future)

This `second-brain` repo will eventually merge into an OpenClaw-powered workflow:
1. Research: Obsidian as the vault, topic files become Obsidian notes
2. OpenClaw reads/writes the vault proactively
3. Claude Code + OpenClaw for development workflows
4. Skills for automated bookmark collection, trend tracking, article digestion
