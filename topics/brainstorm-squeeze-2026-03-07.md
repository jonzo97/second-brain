# Brainstorm Squeeze — 2026-03-07

Structured extract from 4 Google Recorder brainstorm sessions (~50 min total audio).
Organized by theme, not chronologically.

**Sources:**
| Recording | Date | Focus |
|-----------|------|-------|
| Feb 2 @ 9:57 AM | Feb 2 | Weekly planning — work tasks, tool porting, RAG, customer follow-ups |
| Feb 20 @ 10:03 AM | Feb 20 | Project brainstorm — OpenClaw, MIDI/music, Raspberry Pi, RuneScape, income |
| Feb 27 @ 8:05 PM | Feb 27 | Driving to gym — laptop setup, AI pilot program, second brain architecture |
| Feb 27 @ 11:00 PM | Feb 27 | Post-gym — gym tracking, FPGA RAG improvements, NotebookLM, knowledge base |

---

## A. AI Tooling Pilot Program (Coworkers)

**Goal:** Deploy AI coding tools to coworkers — reduce friction, generate goodwill, build internal network.

- **Target coworkers:** Luke (already messaged), Brent/Paul (expressed interest), Mike Cole (already interested)
- **Tool options:**
  - **Claude Code** — "the goat", industry standard, but needs API keys or personal sub
  - **Open Code** — open-source Go-based terminal agent, uses GitHub Copilot OAuth tokens (free corporate tokens)
  - **Continue** (Continuum fork) — UI middle ground between Cursor and pure CLI. Shows diffs, file tree, doesn't require heavy git navigation. Works on MinGW/Windows.
  - **Claude Remote** — set up on work desktop as shared server, let others connect
- **Open questions:**
  - Check with Max: is Continue OK to install, or stick to official Microchip CLI?
  - VPN compatibility: Claude Code doesn't work over VPN — can secure endpoint be accessed from home?
  - Can work desktop run Claude Remote for shared access?
- **Deliverable:** Report to Michael Baxter on pilot program results
- **NotebookLM training:** ~2hr session for coworkers on basics + two-step workflow (Gemini Deep Research → NotebookLM)

**Status:** Still relevant. Package and deploy to coworkers.

---

## B. Second Brain / Open Brain Evolution

**Goal:** Evolve second-brain from flat markdown into a connected, database-backed knowledge system.

- **Database-backed system:** Aligns with Open Brain video direction. Move beyond flat files.
- **GraphDB for connected ideas:** Link brainstorms to projects to tasks. Knowledge base that grows with each interaction.
- **Meta-monitor / heartbeat:** Track status of all projects in one place. Solve the "Monday morning amnesia" problem — come back after the weekend and know exactly where everything stands.
- **Cross-machine sync:** 3 machines (work, home, laptop). Options:
  - Git-based sync (current)
  - Nightly heartbeat cron to auto-sync at midnight
  - Manual sync on work machine + auto-sync on home machine
- **Future improvements tracking via git commit hooks:** On each commit, auto-check off completed future improvements. On marking something as a future improvement, write it to a tracking file. Triggered from CLAUDE.md instructions, not loaded into context unless explicitly accessed.
- **"Loot back" pattern:** After complex multi-prompt work, generate a one-shot prompt to reproduce it next time. Add learnings to knowledge base. Prevents re-doing hard work.
- **Second brain inside .claude?** Considered merging second-brain into `.claude/` folder. **Decision: keep separate.** cc_agents stays public, second-brain stays its own repo.

**Status:** Still relevant. Database migration spike is a medium-priority item.

---

## C. FPGA / Work Projects

### Tool Porting
- **Project 3-1 PR:** Needs rebase on main, full port run to test PLL implementation. Frequency mismatch (6.9 Hz source → best achievable ~4.8 or ~9 Hz) — architectural vs spec-matching decision needed.
- **Meta-prompting improvements:** Biggest contribution opportunity. Add reverse prompting (ask user questions), review step before full porting run. Manuel disagrees on review step but Jon sees value.
- **Justification reports:** Along with generated prompts, produce a human-readable report explaining design decisions. Increases perceived value and user trust.
- **Work trees:** Break down into separate git worktrees for parallel development (project 3-1 + IP configurator branch).

### Tickle Monster
- Personal FPGA CAD tool orchestrator (TCL-based). Parallels tool porting project but more flexible.
- **State:** Working daily but structure is messy. Needs cleanup to become shareable.
- **Goal:** Get to a state where sub-modules can be extracted and shared with coworkers.
- **Knowledge base integration:** Structure scattered knowledge, archive old content, make impressive use cases presentable.

### FPGA RAG
- **Current state:** Working great, very satisfied. Recent blind changes (while watching Sopranos) improved it further.
- **Multi-style embedding:** Better embeddings for tables vs text vs images. Had research on this but not implemented.
- **Image/diagram extraction pipeline:** Missing — can't retrieve diagrams from datasheets. High value if built.
- **Re-enable MCP for Claude Desktop:** Shifted away from MCP to direct Python, but MCP component would enable lighter-weight Claude Desktop usage (especially now that Desktop supports compacting).
- **Document associations:** Link related documents in the RAG for better retrieval.

### Customer Follow-ups (stale — skip)
- ~~Uday follow-up, i-squared (Chris, Patrick, John), SoftConsole + Copilot customer~~
- ~~Monthly report for boss, customer list update~~

### Ethernet Learning
- Topics to cover: 10BASE-T1S, TSN, EtherCAT, RGMII, PHY details
- Conceptual + practical implementation knowledge
- Good candidate for NotebookLM deep dive + flashcard generation

**Status:** Tool porting and FPGA RAG improvements still relevant. Customer follow-ups are stale (Feb 2 items).

---

## D. Automation & Infrastructure

- **NotebookLM podcast automation:** Pre-customer review generation. Pain point: when ready for a walk/break, don't have time to upload + wait for podcast generation. Need a pipeline that pre-generates audio overviews for upcoming customer meetings. Better prompting for "pre-customer review" angle.
- **n8n pipeline:** Text → prompt enhancement → deep research. Send a brief text about something to research → auto-generate high-quality prompt → run through deep research. Raspberry Pi as host.
- **Gemini Deep Research automation:** Script built (`deep_research_runner.py`), uses official Interactions API. Blocked by Google instability (429 errors with zero usage). Retry when Google stabilizes.
- **Spaced repetition review system:** Daily → weekly → monthly review cadence. Trigger reviews automatically. Would help with ADHD-driven forgetting. Live models for flashcard generation getting better (NotebookLM interactive mode already useful).
- **Google Calendar integration for gym tracking:** Label gym sessions with nomenclature, auto-extract via Google Keep or Calendar API. Track workout plans, generate next-day sessions. Alternatively use Gemini CLI for native Google integration.
- **Raspberry Pi 5 as home server:** 8GB or 16GB RAM. Run n8n, OpenClaw, always-on agent services. Need to learn safe server setup.

**Status:** NotebookLM automation and spaced repetition still relevant. n8n and Raspberry Pi are backlog items.

---

## E. Creative / Hobby Projects

### Music
- **Strudel** (s-t-r-u-d-e-l): Worked on it before, never ran/played with results. Revisit with fresh eyes.
- **Max for Live:** Ableton plugins. Underserved market. Dustin (Network) interested — big Ableton user.
- **VCV Rack:** Modular synthesis. Explore programmatic approaches (not just GUI).
- **VST plugins:** Started a VST plugin project before, didn't finish.
- **AI sound generation / sample packs:** Use AI to generate kicks, samples, full sound packs. Programmatic scripting → custom plugin inputs, or actual generation models. Could sell on Gumroad (free + tip jar model).
- **Glitchy audio visualizer:** Inspired by Instagram page doing glitchy audio effects. Cool coding project.

### MIDI Hardware → FPGA Control Surface
- **Hardware:** Novation Launchpad MK1 (8x8 grid) + MIDI Fighter 3D (4x4 grid, DJ Tech Tools)
- **Phase 1:** Computer-based — connect devices, find/write drivers, map buttons to functions, animate LEDs (digital art on the grids)
- **Phase 2:** FPGA demo control surface — connect via MicroBus/USB cape to FPGA/SoC board. Run USB drivers on RISC-V Linux core. Use as interactive control surface for FPGA demos.
- **Phase 3:** FPGA-based polysynth — DSP demo with audio output. Show off DSP capabilities.
- **Why now:** AI coding makes this much more feasible than it used to be.

### RuneScape
- OSRS calculator got 2 stars!
- **Web app improvements:** Live GE price checking, price prediction algorithms, flipping optimization
- **Broader learning:** Good project for practicing frontend/backend, scrapers, financial market analysis basics
- **Maybe:** Videos on niche RuneScape content

### Other
- **Game mod management as AI use case:** Used Claude Code for Hearts of Iron mod management — unpacking, moving files, version string changes, config edits. Perfect application. Unconventional flex.
- **OpenClaw port to RISC-V:** Pie in the sky. Dead PolarFire SoC / BeagleV-Fire boards sitting unused. "Way over my head but interesting."

### Income Goal
- **Target:** $200/month from hobby projects to offset AI subscriptions ($100+ Claude + other tools)
- **Channels:** Gumroad (sound packs, plugins), GitHub stars → reputation → opportunities
- **Philosophy:** Learning is the primary goal, but reducing guilt over subscription costs would be great.

**Status:** All still relevant as hobby/backlog items.

---

## F. Personal Items

Routed to `.personal-todos.md` (gitignored). Not tracked in repo.

---

## Triage: What's Done Since These Recordings

| Item | Status |
|------|--------|
| Google Drive via rclone | **DONE** (set up Feb 20) |
| Google Recorder transcript extraction | **DONE** (manual path, transcripts in hand) |
| cc_agents recipes → skills consolidation | **DONE** |
| Research prompts 01-05 squeezed | **DONE** |
| Progressive tool discovery terminology | **DONE** (in research extracts) |
| Second brain inside .claude decision | **RESOLVED** (stays separate) |
| Cross-project mailbox improvements | **STILL RELEVANT** |
| mchp_mcp_tools → skills migration | **STILL RELEVANT** |
| Tickle Monster cleanup | **STILL RELEVANT** |
| Customer follow-ups (Uday, i-squared, SoftConsole) | **STALE** (Feb 2 items, skip) |
| Monthly report, customer list update | **STALE** (skip) |
| LinkedIn posts drafting | **STALE** (skip) |
