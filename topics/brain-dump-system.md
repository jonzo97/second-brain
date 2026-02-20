# Brain Dump Ingestion System

A system to capture, process, and action Jon's voice-recorded brain dumps so nothing gets lost.

## Current Workflow (Broken)

```
Google Recorder → transcript → paste into Claude chat → LOST FOREVER
```

**Three distinct problems:**
1. **Lost conversations**: Ideas, tasks, and insights get buried in a sea of Claude chats and are never resurfaced
2. **Repetition without action**: The same topics (e.g., LinkedIn series) come up in brain dump after brain dump without progressing to execution. Has discussed LinkedIn posts at least 6 times without writing one.
3. **Scattered technical knowledge**: Valuable debugging sessions, architecture decisions, and research deep-dives spread across dozens of Claude chats with no way to find them later

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

## Repetition Detection (Critical Feature)

The biggest failure mode: discussing the same thing repeatedly without acting.

### How It Should Work
1. When processing a new brain dump, compare extracted topics against previous dumps
2. If a topic has appeared 3+ times without a corresponding completed action: **FLAG IT**
3. Present as: "You've mentioned [topic] X times. Here's the smallest possible next step to break the loop."
4. The "smallest possible step" is key - not "write the LinkedIn series" but "spend 5 minutes voice-recording your origin story"

### Why This Matters for ADHD
- ADHD brains often get stuck in the planning/rumination loop
- Talking about something feels like progress but isn't
- The system needs to be the external accountability that the brain can't provide
- Don't shame, just nudge: "This keeps coming up. Want to spend 10 minutes on it right now?"

---

## Claude Chat History → RAG (Side Project)

**Goal**: Download Claude conversation history, ingest into a RAG system, and mine it for:
- Recurring ideas and project concepts
- Technical learnings and solutions
- Patterns in what keeps coming up (more repetition detection)
- Lost gems that were discussed once and forgotten

### Research Needed
- [ ] Can Claude chat history be exported? (Check account settings, API)
- [ ] What format does it export in? (JSON? Markdown?)
- [ ] ChromaDB recipe from cc_agents is directly relevant here
- [ ] Token budget concern: need to do this WITHOUT nuking weekly API tokens
- [ ] Could process offline with local model (LM Studio) to save tokens
- [ ] Or use Haiku 4.5 which is cheap for ingestion/indexing

### Integration with Second Brain
- Extracted insights feed into topic files
- Recurring themes get surfaced and tracked
- Technical solutions get indexed for future reference

---

## Spaced Repetition for Technical Learning

**Goal**: Build a review system for technical learnings so Jon retains terminology and concepts (important for "not sounding dumb" in professional contexts).

### Concept
- After learning something new, create a review card (term + explanation)
- Review daily for 1 week, then weekly for 1 month
- Focus on: right terminology, key concepts, framework names, architecture patterns
- Could be simple markdown flashcards or a proper SRS tool

### Research Needed
- [ ] Anki or similar SRS tools that integrate with markdown?
- [ ] Could NotebookLM-generated podcasts serve as passive spaced repetition?
- [ ] OpenClaw skill that quizzes you via Telegram/WhatsApp?
- [ ] Even a simple daily email/notification with 3 review items would help

### Why This Matters
- Technical conversations at work require precise terminology
- "I know how this works but can't name it" undermines credibility
- Spaced repetition is the most evidence-based learning technique
- Pairs perfectly with the passive learning pipeline (podcasts reinforce, SRS tests retention)

---

## This Repo IS a Brain Dump Venue

This Claude Code session is itself a brain dump that gets captured in real time. Unlike Claude.ai chats that scroll away, everything said here becomes:
- Committed to git (searchable, versioned, permanent)
- Organized into topic files (findable)
- Actionable (checkboxes, research tasks)

**Pattern to encourage**: When having a brain dump moment, open Claude Code in this repo and just talk. The conversation becomes structured notes automatically.

---

## Integration Points

- **Google Drive**: Store raw recordings and processed outputs
- **Obsidian**: Brain dump notes as daily entries
- **OpenClaw**: Auto-process new recordings, surface insights
- **This repo**: Archive of extracted ideas feeding into topic files (and a brain dump venue itself)
- **Claude Code**: Process transcripts during dev sessions
- **Claude Chat History**: Export and mine for lost ideas and patterns
- **Spaced Repetition**: Feed technical learnings into review system
