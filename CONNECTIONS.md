# How Everything Connects

A map of how all the side projects, tools, and systems feed into each other. Useful for seeing the big picture and finding leverage points where one thing unblocks many.

## The Core Loop

```
Brain Dump (voice) → Process → Organize → Surface → ACT → Learn → Brain Dump
```

If any link in this chain breaks (especially "Surface" and "ACT"), everything stalls.

## System Map

```
┌─────────────────────────────────────────────────────────┐
│                    INPUT CHANNELS                        │
│                                                         │
│  Morning Brain Dumps ──┐                                │
│  (Google Recorder)     │                                │
│                        ├──→ PROCESSING ──→ STORAGE      │
│  Claude Code Sessions ─┤    (Haiku/Gemini)   │          │
│  (like this one)       │         │           │          │
│                        │    Extracts:        ▼          │
│  Claude Chat History ──┘    • Action items   second-brain│
│  (export → RAG)             • Ideas          repo       │
│                             • Questions      Obsidian   │
│  YouTube Channels ────────→ • Summaries      Google Drive│
│  (transcript digest)                                    │
│                                                         │
│  Perplexity Research ─────→ Weekly roundups              │
│  Anthropic Blog ──────────→ Digested posts              │
│  HuggingFace/GitHub ──────→ Trend snapshots             │
└─────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────┐
│                   SURFACING LAYER                        │
│                   (The ADHD-critical part)               │
│                                                         │
│  "What should I work on?" ──→ Low-hanging fruit by mood │
│  Repetition detection ──────→ "You've said this 6x..."  │
│  Spaced repetition ─────────→ Daily terminology review  │
│  NotebookLM podcasts ───────→ Passive learning at gym   │
│  OpenClaw proactive alerts ─→ Push, don't wait for pull │
└─────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────┐
│                    OUTPUT / ACTION                       │
│                                                         │
│  Code ──────────→ cc_agents, MCP servers, side projects │
│  Writing ───────→ LinkedIn series, docs, brain dumps    │
│  Learning ──────→ Courses, podcasts, spaced repetition  │
│  Career ────────→ Network, collaborators, differentiation│
└─────────────────────────────────────────────────────────┘

## What Unblocks What

Understanding dependencies helps prioritize:

### Tier 1: Foundation (Do First)
These unblock everything else:

| Task | Unblocks |
|------|----------|
| Google Drive organization | Quick podcast access, brain dump storage, file organization |
| Generate first NotebookLM podcasts (Docker, Node.js) | Passive learning at gym, learning fundamentals |
| Remote Claude Code setup (SSH for second-brain) | Working on projects from anywhere |
| Brain dump processing prompt (MVP) | Stop losing ideas, detect repetition |

### Tier 2: Multipliers (Do Next)
These amplify everything from Tier 1:

| Task | Amplifies |
|------|-----------|
| OpenClaw on a device | Proactive surfacing, always-on assistant |
| Obsidian vault setup | Better organization, graph connections, OpenClaw integration |
| Claude history → RAG | Mine past conversations for lost ideas |
| N8N + Telegram hook | Remote Claude Code access, notifications |
| LinkedIn first post | Career positioning, finding collaborators (break the 6x loop!) |

### Tier 3: Power-Ups (When Ready)
These are cool but not urgent:

| Task | Adds |
|------|------|
| RISC-V OpenClaw challenge | Fun, learning, unique flex |
| Full automation pipeline (YouTube → digest → store) | Automated trend tracking |
| Spaced repetition system | Better retention of terminology |
| Perplexity scheduled research | Passive knowledge gathering |

## Project Interconnections

```
second-brain ←──→ cc_agents (cross-project mailbox, shared patterns)
     │                │
     ├── OpenClaw ────┤ (orchestration layer for both)
     │                │
     ├── Obsidian ────┤ (storage layer for both)
     │                │
     └── Google Drive ┘ (file storage, podcasts, brain dumps)

LinkedIn Series ←── second-brain (content source)
                ←── cc_agents (technical examples)
                ←── Brain dumps (raw material via voice)

Learning Pipeline:
  learning.md topics → NotebookLM podcasts → Google Drive → Phone → Gym
  learning.md topics → Spaced repetition → Daily review → Retention
  Anthropic blog → Haiku digest → Action items → Projects
```
