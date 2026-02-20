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
