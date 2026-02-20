# Brain Dump Ingestion System

A system to capture, process, and action Jon's voice-recorded brain dumps so nothing gets lost.

## Current Workflow (Broken)

```
Google Recorder → transcript → paste into Claude chat → LOST FOREVER
```

The problem: Claude chats are ephemeral. Ideas, tasks, and insights get buried in a sea of conversations and are never resurfaced.

## Ideal Workflow

```
Google Recorder (voice dump, 15-20 min)
       ↓
Transcript extraction (automatic)
       ↓
AI Processing (Haiku 4.5 / Gemini)
  ├── Extract action items → TodoWrite / task list
  ├── Extract ideas → second-brain topic files
  ├── Extract problems/blockers → flag for next session
  ├── Extract questions → research queue
  └── Generate summary → daily log
       ↓
Store in organized location (Obsidian / Google Drive / this repo)
       ↓
Surface relevant items when Jon asks "what should I work on?"
```

## Components to Build

### 1. Transcript Capture
- [ ] Google Recorder already generates transcripts on Pixel 10 Pro
- [ ] Research: Can transcripts auto-sync to Google Drive?
- [ ] Research: Can we auto-detect new recordings and trigger processing?
- [ ] Alternative: dedicated voice-to-text app that outputs directly to a folder

### 2. Processing Pipeline
- [ ] Template prompt for brain dump digestion (extract categories above)
- [ ] Could run through Claude API (Haiku for cost efficiency)
- [ ] Or Gemini (already on the phone, could process locally)
- [ ] n8n could orchestrate: detect new transcript → process → store results

### 3. Storage & Organization
- [ ] Daily summaries in a `brain-dumps/` folder (date-stamped)
- [ ] Action items extracted to a running task list
- [ ] Ideas tagged and routed to relevant topic files
- [ ] Full transcripts kept as archive

### 4. Resurfacing (The ADHD-Critical Part)
- [ ] "What should I work on?" command that pulls from:
  - Extracted action items (prioritized)
  - Low-hanging fruit from across all topics
  - Things that match current mood/energy
- [ ] OpenClaw could proactively surface things based on context
- [ ] Daily/weekly digest pushed to phone

## Quick Win (MVP)

The simplest version that would already help:

1. After a brain dump, paste transcript into a Claude chat with a standard prompt
2. Prompt extracts: action items, ideas, questions, summary
3. Manually copy results into this repo or Obsidian

**Standard prompt to create:**
```
Here's my brain dump transcript from [date]. Please extract:
1. ACTION ITEMS - specific things I need to do, with priority
2. IDEAS - things to explore or research later
3. PROBLEMS - blockers or issues I mentioned
4. QUESTIONS - things I need to figure out
5. SUMMARY - 3-5 sentence overview of what's on my mind

Format each section as a markdown checklist.
```

## Integration Points

- **Google Drive**: Store raw recordings and processed outputs
- **Obsidian**: Brain dump notes as daily entries
- **OpenClaw**: Auto-process new recordings, surface insights
- **This repo**: Archive of extracted ideas feeding into topic files
- **Claude Code**: Process transcripts during dev sessions
