# Workflow & Automation Ideas

Future automation pipelines to build. These are ideas, not implementations yet.

---

## YouTube AI Channel Digest Pipeline

**Goal**: Periodically scrape AI YouTube channels for actionable insights, auto-summarize, and feed into second brain.

### Channels to Track
- [ ] [IndyDevDan](https://www.youtube.com/@indydevdan) - Claude Code, agentic coding patterns
- [ ] [Two Minute Papers](https://www.youtube.com/@TwoMinutePapers) - AI/ML research paper breakdowns
- [ ] _Add more as you remember them_

### Transcript Extraction Options

| Approach | Pros | Cons |
|----------|------|------|
| **Gemini CLI** | Native YouTube transcript support, Jon has Gemini Pro sub | May not have API keys, CLI availability unclear |
| **Gemini API via OpenRouter** | Pay-per-use, no separate sub needed | Adds cost, extra routing layer |
| **yt-dlp + whisper** | Free, local, no API needed | Slower, needs GPU for good whisper, extra steps |
| **youtube-transcript-api** (Python) | Free, pulls existing captions directly | Only works if captions exist, no auto-transcription |
| **NotebookLM** | Good at YouTube digestion, already bookmarked | Manual, not scriptable (unless MCP works) |

### Processing Pipeline (Ideal)
1. **Scrape**: Pull new videos from tracked channels (RSS feeds or YouTube API)
2. **Transcribe**: Get transcripts (Gemini, yt-dlp, or caption API)
3. **Digest**: Run through Haiku 4.5 or Gemini for summaries + action items
4. **Store**: Write to Obsidian vault / second-brain repo as structured notes
5. **Surface**: OpenClaw proactively flags relevant insights

### Open Questions
- Does Gemini Pro sub include CLI access or API keys?
- Can Gemini CLI be scripted/automated?
- Best way to detect "new video" triggers (RSS? cron? n8n?)

---

## Perplexity Automated Research

**Goal**: Use Perplexity Pro subscription for automated daily/weekly research sweeps.

### What Jon Has
- Free 1-year Perplexity Pro subscription
- Perplexity supports scheduled searches / "Spaces"

### Potential Uses
- [ ] Weekly AI landscape sweep (new tools, trending repos, breaking papers)
- [ ] Daily news digest for specific topics (MCP, Claude updates, FPGA + AI)
- [ ] Competitor/tool monitoring (track specific projects for updates)
- [ ] Research queries that feed into second-brain topics

### Integration Questions
- Does Perplexity have an API? (Pro may include API access)
- Can Perplexity Spaces export to markdown/JSON?
- Could pipe Perplexity outputs into Obsidian via webhook or n8n?
- OpenClaw integration possible?

---

## Subscriptions & Tools Available

Tracking what Jon has access to for building pipelines.

| Tool | Subscription | API Access? | Notes |
|------|-------------|-------------|-------|
| Claude (Anthropic) | Pro / API | Yes | Primary AI, Claude Code |
| Gemini (Google) | Pro | Unknown | Good at YouTube transcripts |
| Perplexity | Pro (1yr free) | Check | Daily/weekly research automation |
| OpenRouter | Pay-per-use | Yes | Multi-model routing |
| HuggingFace | Free account (jonzo97) | Yes | Models, spaces, datasets |
| n8n | Self-hosted | N/A | Workflow automation (Docker) |
| GitHub | Account | Yes | Repos, actions |
| **GitHub Copilot** | **Corporate** | **Yes (OAuth)** | **Free tokens! See leverage section below** |
| **M365 Copilot** | **Corporate** | **Check** | **Enterprise AI features, mostly Office integration** |

---

## "What Should I Work On?" System

**The ADHD-critical feature.** When Jon has downtime and momentum, present options by effort/interest so he can just pick and go.

### Concept
A command or prompt that scans across all topic files and surfaces:
- **Quick wins** (~5-15 min): Install something, read a short article, check out a repo
- **Medium tasks** (~30-60 min): Set up a tool, work through a tutorial, write a draft
- **Deep dives** (~2+ hrs): Build a pipeline, configure infrastructure, write an article

### Filtered by mood/context:
- **"I'm at the gym"** → Podcasts to listen to, articles to read on phone
- **"I'm at my desk with energy"** → Build something, configure something
- **"I'm in bed, low energy"** → Light reading, YouTube videos, brainstorming
- **"I have 10 minutes"** → Quick installs, bookmark reviews, one-off tasks

### Implementation Options
- [ ] Simple: a script that scans `- [ ]` items across all topic files and categorizes
- [ ] Medium: Claude Code skill that reads repo and presents prioritized options
- [ ] Full: OpenClaw skill that proactively suggests based on time of day and context

### Date & Time Awareness
Should use system date/time to:
- Track when items were added (staleness)
- Know time of day for context-appropriate suggestions
- Track streaks / consistency

---

## Future Pipeline Architecture

```
YouTube Channels ──┐
                   ├── Transcript extraction (Gemini CLI / yt-dlp)
Perplexity ────────┤
                   ├── Digest & summarize (Haiku 4.5 / Gemini)
RSS Feeds ─────────┤
                   ├── Store (Obsidian vault / second-brain repo)
Anthropic Blog ────┘
                   └── Surface (OpenClaw proactive alerts)
```

### Orchestration Options
- **n8n**: Already self-hosted, visual workflows, good for scheduled tasks
- **GitHub Actions**: Free for public repos, cron triggers, good for this repo
- **OpenClaw skills**: Once set up, could be the orchestration layer itself
- **Plain cron + scripts**: Simplest, most reliable, least fancy

---

## Claude Code + N8N via Messaging Hook

**Goal**: Control Claude Code remotely via Telegram or WhatsApp through n8n as the middleware.

### Concept
- n8n listens for incoming Telegram/WhatsApp messages
- Parses commands and triggers Claude Code (via API or CLI)
- Returns results back through the messaging channel
- Enables kicking off tasks, checking status, reviewing PRs from phone

### Research Needed
- [ ] How does n8n's Telegram node work? Can it handle bidirectional chat?
- [ ] Can Claude Code CLI be invoked from n8n (shell execute node)?
- [ ] Alternatively: use Claude API directly from n8n (HTTP request node)
- [ ] Check `RichardAtCT/claude-code-telegram` (trending on GitHub) - might already solve this
- [ ] Security: how to auth so only Jon can trigger it

### Why This Matters
This would bridge the gap between "at my desk" and "on the go" - could review code, run builds, or ask Claude to research something from the gym or bed.

---

## Mobile / Remote Claude Code Setup

**Goal**: Use Claude Code from phone, tablet, or any device away from main workstation.

### The Problem
- Most projects need heavy local tooling (FPGA tools, Python envs, etc.)
- Claude Code desktop/mobile apps exist but need SSH to a dev machine
- Don't know how to set up cloud environments or SSH connections for this yet

### Options to Research

| Approach | Pros | Cons |
|----------|------|------|
| **SSH to home machine** | Free, all tools already installed | Need port forwarding or tailscale, machine must stay on |
| **SSH to work machine** | Has FPGA tools | VPN/firewall complications, IT policy |
| **Cloud VM (AWS/GCP/Azure)** | Always on, clean environment | Monthly cost, need to install toolchains |
| **GitHub Codespaces** | Integrated with repos, easy setup | Limited to what fits in container, $/hr |
| **Tailscale + existing machine** | Easy mesh VPN, no port forwarding | Still need a machine running somewhere |
| **Mini PC as always-on server** | One-time cost, dedicated, at home | Another device to maintain |

### Research Tasks
- [ ] How does Claude Code desktop/mobile SSH work? What's the setup process?
- [ ] How are other people configuring remote Claude Code? Search for guides/posts
- [ ] What's the minimum viable cloud setup? (cheapest VM that can run my toolchains)
- [ ] Can Tailscale make SSH from phone to home machine painless?
- [ ] Which of my projects could work in a cloud/container env vs. need local tools?

### Priority Projects for Remote Access
1. **second-brain** (this repo) - lightweight, markdown-only, great test case
2. **cc_agents** - the agentic framework, high value, needs Python + Claude Code
3. Everything else after these two are working

### Priority
This is high priority - the faster this is set up, the more downtime becomes productive time (gym, lunch, bed, commute). Even getting ONE project accessible remotely would be a big win. Start with second-brain (simplest) then cc_agents (most valuable).

---

## Side Projects: Hardware Hosts

### OpenClaw Deployment Candidates

Devices Jon has or is considering for running OpenClaw as an always-on agent:

| Device | Status | Pros | Cons |
|--------|--------|------|------|
| **Old laptop** | Has it, could leave at work | Full OS, WiFi, battery backup | Bulky, power draw |
| **Steam Deck** | Has it | Portable, Linux, decent specs | Overkill? Gaming device |
| **Raspberry Pi** | Considering buying this weekend | Cheap, low power, official guide exists | Limited RAM/CPU |
| **Mini PC** | Considering (GMKtec in bookmarks) | Powerful, small, always-on | Cost |
| **RISC-V dev kits** | Has them, not actively using | Fun challenge, unique | Untested, likely painful |

### RISC-V Challenge (Fun Project)

**Goal**: Get OpenClaw or similar agent running on RISC-V hardware.

**Available dev kits:**
- [ ] PolarFire SoC Icicle Kit (PIC64-GX) - Microchip RISC-V + FPGA
- [ ] BeagleV-Fire Kit - BeagleBoard RISC-V + FPGA
- [ ] (Any other RISC-V boards in the collection?)

**Why**: Fun challenge, learning experience, unique flex, and these boards are sitting unused.

**Challenges**: Node.js on RISC-V (OpenClaw is TypeScript/Node), limited packages, may need cross-compilation. SQLite should work but vector embeddings might be tricky.

---

## Corporate Subscription Leverage ("Free Tokens")

**Goal**: Maximize value from corporate-provided AI subscriptions. These are essentially free tokens — find projects that use them heavily.

### What Jon Has (Corporate)

| Subscription | What It Gives You | How to Leverage |
|-------------|-------------------|-----------------|
| **GitHub Copilot** | OAuth tokens for AI models (GPT-4o, Claude variants, Gemini) | Use with OpenCode or copilot-api proxy |
| **M365 Copilot** | Enterprise AI in Office suite | Research deeper — may have API hooks for automation |

### OpenCode — Use Copilot Tokens for Claude-Like Workflows
- [ ] [OpenCode](https://opencode.ai/) - Open-source terminal AI coding agent (Go-based)
- 75+ LLM providers including GitHub Copilot via OAuth device flow
- Run `/connect` → choose GitHub Copilot → authenticate at `github.com/login/device`
- Gets access to GPT-4o, Claude variants, Gemini through Copilot sub
- **Note**: Original author moved on, project continuing as "Crush" with Charm team — monitor stability
- [ ] Test OpenCode with corporate Copilot OAuth — see what models are accessible
- [ ] Compare OpenCode vs Claude Code for different task types

### copilot-api Proxy (Higher Risk, More Flexible)
- [ ] [copilot-api](https://github.com/ericc-ch/copilot-api) - 2.5k stars, reverse-engineered proxy
- Exposes Copilot as OpenAI-compatible (`/v1/chat/completions`) AND Anthropic-compatible (`/v1/messages`) endpoints
- Run `npx copilot-api@latest start --claude-code` for one-command Claude Code integration
- **WARNING**: GitHub ToS prohibit excessive automated use — account suspension risk is real
- May be better suited for personal experimentation than corporate use

### 9router (Multi-Provider Routing)
- [ ] [9router](https://github.com/decolua/9router) - Smart proxy/router for multiple AI backends
- 3-tier fallback (subscription > budget > free), format translation, multi-account load balancing
- Could combine Copilot + OpenRouter + Claude API into one unified endpoint

### Project Ideas to Burn Free Tokens
- [ ] Code review automation on side projects (Copilot tokens are free, burn them on reviews)
- [ ] Automated PR descriptions and commit message generation
- [ ] Copilot-powered linting and test generation for cc_agents
- [ ] Use OpenCode for second-brain maintenance tasks (cheaper than Claude Code API)
- [ ] Research: what M365 Copilot APIs exist — any way to pipe data into/out of it?

### Important Context
On Jan 9, 2026 Anthropic blocked third-party tools from using Claude subscription OAuth tokens (reverse-subscription abuse). This does NOT affect Copilot → Claude proxying, but means you can't reverse-proxy a Claude Pro sub to avoid API costs.

---

## Claude Code Auto-Run & Scheduling

**Goal**: Run Claude Code tasks automatically — nightly project checks, scheduled research, CI integration.

### cc-caffeine (Sleep Prevention)
- [ ] [cc-caffeine](https://github.com/samber/cc-caffeine) - Prevents computer sleep while Claude Code works
- Client-server with Electron, system tray, JSON-file IPC
- Sessions auto-expire after 15 minutes of inactivity
- Integrates via Claude Code hooks (UserPromptSubmit, PreToolUse, PostToolUse)
- **18 stars, v0.2.0 (Oct 2025)** — small utility, not an automation framework
- Useful for: long laptop sessions where sleep would kill a running agent

### Headless Claude Code (`claude -p`)
The official way to run Claude Code programmatically:
```bash
claude -p "Check all project git statuses" --allowedTools "Read,Bash" --output-format json
```
- `--continue` / `--resume <session_id>` for chained conversations
- `--output-format json` or `stream-json` for structured results
- `--allowedTools` with prefix matching
- `--append-system-prompt` for custom instructions
- Python and TypeScript SDK packages also available

### Scheduling Options
- [ ] **cron + `claude -p`**: Simplest. Wrap in shell script, invoke from cron
- [ ] [claude-code-scheduler](https://github.com/jshchnz/claude-code-scheduler) - Uses `claude -p` with `--dangerously-skip-permissions`
- [ ] [runCLAUDErun](https://runclauderun.com/) - macOS-native scheduler app
- [ ] [CCAutoRenew](https://github.com/aniketkarne/CCAutoRenew) - Daemon manager with scheduled stop/restart
- [ ] **GitHub Actions** - `anthropics/claude-code-action` for CI/CD integration
- [ ] [Feature Request #4785](https://github.com/anthropics/claude-code/issues/4785) - Native cron-like hooks (not yet implemented)

### Nightly Project Health Check (Idea)
Use `claude -p` on a cron to scan all projects nightly:
```bash
# Example: nightly-check.sh
claude -p "Check git status of ~/second-brain, ~/cc_agents, ~/meta-project. Report uncommitted changes, stale branches, and pending todos." \
  --allowedTools "Bash,Read,Glob" \
  --output-format json > /tmp/nightly-report.json
```
Could pipe results to Telegram via n8n, or store in second-brain as a daily log.

---

## Inter-Project Communication Protocols

**Goal**: Get Claude Code sessions in different projects to coordinate without manual copy-paste.

### Current State
- `~/.claude/cross-project.md` exists as a manual mailbox (cc_agents ↔ second-brain)
- Works but is ad-hoc and requires reading/writing manually
- No standardized protocol for structured task delegation

### Patterns Explored

**File-based mailbox (current)**
- Shared markdown or JSON files that agents poll
- Simple, works anywhere, no infrastructure
- Limited: no notifications, no structured schema, easy to miss messages

**Agent Teams (official, experimental)**
- Shared task list at `~/.claude/tasks/{team-name}/`
- Mailbox at `~/.claude/teams/{team-name}/`
- Enables lead + teammate pattern with direct messaging
- **Limitation**: session-scoped, single-repo by default, no cross-repo teams yet
- [Feature Request #4689](https://github.com/anthropics/claude-code/issues/4689) - Dynamic context management across projects (open)

**Shared MCP servers**
- Multiple projects connect to same MCP server for shared state
- Could use memory MCP, graph-db MCP, or custom project-status MCP
- Already have memory MCP configured for ~/meta-project

**GitHub Issues as task database**
- [ccpm](https://github.com/automazeio/ccpm) uses GitHub Issues for cross-agent task tracking
- Each issue = a task, agents claim and update via gh CLI
- Nice audit trail, accessible from anywhere

### The Mega Second-Brain / Monorepo Question

**Idea**: Instead of separate repos with cross-project messaging, consolidate into one mega repo with git worktrees and branches.

**Pros:**
- Single context, single Claude Code session can see everything
- Git worktrees give isolation without separate repos
- No inter-project communication needed if it's all one project
- Easier to search, link, and cross-reference

**Cons:**
- Mixing very different concerns (markdown second-brain vs Python cc_agents vs FPGA projects)
- Git history becomes cluttered
- Different toolchains per project (Python, Node, Tcl, etc.)
- Permission boundaries blur (work-internal stuff in same repo as public content)

**Hybrid approach worth exploring:**
- Keep repos separate but use a shared orchestration layer
- `~/meta-project` or second-brain as the "brain" that monitors others
- Claude Co-Work might be the right tool for this (multi-file, research-oriented)
- Graph database to model relationships between projects (see learning.md)

### Research Tasks
- [ ] Formalize the cross-project.md mailbox protocol (schema, read/write conventions)
- [ ] Test Agent Teams across two repos (is it possible? workarounds?)
- [ ] Evaluate if meta-project should merge into second-brain
- [ ] Research Claude Co-Work for multi-project monitoring use case
- [ ] Try git worktrees within second-brain for experimental branches

---

## Meta-Project Monitoring

**Context**: Jon has been using `~/meta-project` to monitor all side projects by analyzing git statuses. Exploring whether to migrate this into second-brain or Claude Co-Work.

### What meta-project Does (Current)
- Analyzes git status across multiple project directories
- Was exploring Anthropic MCP and/or graph-db approaches for cross-project knowledge
- Has memory MCP configured (`.mcp.json` with `@modelcontextprotocol/server-memory`)
- Knowledge graph stored at `~/.claude/knowledge_graph.json`

### Migration Options

| Destination | Pros | Cons |
|-------------|------|------|
| **Keep in meta-project** | Already set up, isolated context | Another repo to maintain, easy to forget about |
| **Merge into second-brain** | Single source of truth, already the "brain" | Adds complexity to a mostly-markdown repo |
| **Claude Co-Work** | Designed for multi-file research, always-on | Unknown capabilities, may not support git monitoring |
| **Nightly cron (`claude -p`)** | Automated, no manual intervention | Need to set up headless execution first |

### Research Tasks
- [ ] Audit what's actually in ~/meta-project — what's useful vs. abandoned?
- [ ] Test if Claude Co-Work can monitor git repos and generate reports
- [ ] Design a nightly `claude -p` script that replicates meta-project's monitoring
- [ ] Decide: merge, migrate, or keep separate?
