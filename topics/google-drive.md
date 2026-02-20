# Google Drive & Mobile Workflow

Leveraging 2TB Google Drive + Pixel 10 Pro + Gemini for quick access to learning materials and second brain content.

## The Problem

- Paying for 2TB Google Drive storage, barely using it
- NotebookLM generates great podcasts but they're hard to access quickly
- Google Drive is disorganized
- Need things accessible in <10 seconds from phone or they won't get used
- Pixel 10 Pro has Gemini built-in as assistant - should be able to pull up files by voice

## Google Drive Organization (TODO)

### Proposed Structure
```
My Drive/
├── Second Brain/
│   ├── NotebookLM Podcasts/
│   │   ├── Docker Fundamentals.mp3
│   │   ├── Node.js Basics.mp3
│   │   ├── React + Vercel.mp3
│   │   ├── SSH & Cloud Dev.mp3
│   │   └── ...
│   ├── Brain Dumps/
│   │   ├── Raw Recordings/
│   │   ├── Transcripts/
│   │   └── Processed/
│   ├── Research/
│   │   ├── Anthropic Blog Digests/
│   │   └── Weekly AI Roundups/
│   └── Reading List/
│       └── Saved articles, PDFs, etc.
├── Projects/
│   └── (project-specific files)
└── (existing stuff, organized eventually)
```

### Quick Access Workflow (Ideal)

**At the gym / walking / commuting:**
1. "Hey Google, play my Docker podcast from Drive"
2. Gemini assistant finds the MP3 in the organized folder
3. Start learning passively

**Having an idea:**
1. Open Google Recorder, brain dump
2. Recording auto-syncs to Drive/Second Brain/Brain Dumps/
3. Gets processed later (manually or via automation)

**Checking what to work on:**
1. Open second-brain repo on phone (GitHub mobile)
2. Or ask OpenClaw via Telegram/WhatsApp "what's my low-hanging fruit?"

## NotebookLM Podcast Pipeline

### Podcasts to Generate (from learning.md)
- [ ] Docker fundamentals
- [ ] Node.js basics
- [ ] React + Vercel
- [ ] SSH & cloud dev setup
- [ ] MCP deep dive
- [ ] Claude Agent SDK
- [ ] OpenClaw architecture
- [ ] (generate more as topics are identified)

### Process
1. Gather source material for topic (docs, articles, blog posts)
2. Feed into NotebookLM
3. Generate audio overview / podcast
4. Export MP3 to Google Drive (organized folder)
5. Accessible via Gemini assistant on phone

## Gemini + Pixel Integration

### What Should Work
- Gemini assistant can search and open Google Drive files
- "Play [filename]" should work for audio files
- Could potentially ask Gemini to summarize Drive documents
- All under same Google account = seamless auth

### Research Needed
- [ ] Can Gemini assistant play specific MP3s from Drive by voice command?
- [ ] Does Gemini have good Drive file search?
- [ ] Can NotebookLM podcasts be auto-exported to a Drive folder?
- [ ] Is there a way to create a "podcast playlist" from Drive MP3s?

## OpenClaw + Google Drive (Future)

OpenClaw has potential Google Drive integration but **security is a concern**:
- Drive has personal files, financial docs, etc.
- OpenClaw skills have known credential leak issues (7.1% per Snyk)
- Need to scope access carefully (maybe read-only, specific folders only)
- Could use Google Drive API with limited OAuth scopes

### Safety Requirements
- [ ] Read-only access to specific folders only
- [ ] No access to personal/financial folders
- [ ] Audit trail of what's accessed
- [ ] Revokable permissions
- [ ] Don't install random ClawHub skills that request Drive access

## Claude Co-Work for Drive Organization?

Would love to use Claude to help organize Google Drive but:
- [ ] Research: Does Claude desktop app have Google Drive integration?
- [ ] Research: Is there an MCP server for Google Drive?
- [ ] Research: Could n8n + Google Drive API handle bulk organization?
- [ ] Alternative: Just do it manually with a checklist (boring but safe)
