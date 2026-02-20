# Dev Tools & IDEs

Editors, testing tools, and developer productivity.

## Editors & IDEs

- [ ] [Zed](https://zed.dev/) - Fast, collaborative code editor
- [ ] [Theia IDE](https://theia-ide.org/) - AI-native open-source cloud & desktop IDE
- [ ] [GitHub Copilot Features](https://github.com/settings/copilot/features) - Copilot settings & features

## LLM Testing & Evaluation

- [ ] [promptfoo](https://www.promptfoo.dev/) - Secure & reliable LLM testing/evaluation

## Claude Code

- [ ] [Claude Code](https://claude.ai/code) - Anthropic's CLI coding agent
- [ ] [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - Complete Claude Code config collection (agents, skills, hooks, commands, rules, MCPs)
- [ ] [Official VSCode Extension](https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code) - First-party Claude Code in VSCode (requires VSCode 1.98+)

## Terminal & IDE Setup for Claude Code

**Current pain point**: Windows Terminal has multiple known issues with Claude Code. Researching better options, especially for parallel sessions.

### Terminal Comparison

| Terminal | Platform | Shift+Enter | Agent Teams Split-Pane | Notes |
|----------|----------|-------------|----------------------|-------|
| **Ghostty** | macOS/Linux | Native ✓ | No | Best rendering, lowest memory, community favorite for Claude Code |
| **iTerm2** | macOS | Native ✓ | Yes ✓ | Best tmux integration, required for split-pane Agent Teams |
| **WezTerm** | Cross-platform | Native ✓ | No | WebGPU rendering, Lua scripting, good for programmatic control |
| **Kitty** | macOS/Linux | Native ✓ | No | GPU-accelerated, highly configurable |
| **Alacritty** | Cross-platform | Needs setup | No | Fastest/lightest (~30MB), no tabs (pair with tmux) |
| **Windows Terminal** | Windows | Broken (Ctrl+Enter instead) | No | Multiple bugs: ConPTY freezes, PATH conflicts, input hangs |
| **Warp** | macOS/Linux | Needs setup | No | Has its OWN agent (competes with Claude Code, not a host for it) |

### Windows Terminal Known Issues
- [ ] VSCode integrated terminal freezes with native installer (`claude.exe`) - ConPTY issue ([#24584](https://github.com/anthropics/claude-code/issues/24584))
- [ ] Input freezes after launch with prompt argument ([#22969](https://github.com/anthropics/claude-code/issues/22969))
- [ ] Shift+Enter doesn't work, need Ctrl+Enter ([#21360](https://github.com/anthropics/claude-code/issues/21360))
- [ ] Desktop installer PATH hijacks npm CLI ([#25075](https://github.com/anthropics/claude-code/issues/25075))
- [ ] Co-Work on Windows 11 Home broken for some users ([#24918](https://github.com/anthropics/claude-code/issues/24918))

### VSCode Extension (Official - Recommended)
The `anthropic.claude-code` extension is now the recommended IDE integration:
- Shared conversation history with CLI (`claude --resume` continues extension conversations)
- Inline diff review, plan mode, auto-accept mode
- @-mention files with line ranges, checkpoints/rewind
- Multiple conversations in separate tabs or windows (parallel sessions!)
- Context indicator shows window usage in prompt box
- **Also installable in Cursor**: `cursor:extension/anthropic.claude-code`
- Limitation: no `!` bash shortcut, no tab completion, no split-pane Agent Teams

### Cursor IDE ("Best of Both Worlds")
- [ ] Research Cursor as Claude Code host
- VSCode fork with native AI completions + inline diffs + AI-powered search
- Install Claude Code extension inside Cursor for dual AI: Cursor's tab completions for in-flow coding + Claude Code's deep reasoning for architecture/refactoring
- Claude Code uses **5.5x fewer tokens** than Cursor for identical tasks (independent testing)
- **Cost**: Free Hobby tier (limited), Pro ~$20/month, Teams $40/user/month
- **Decision needed**: Is the dual-AI benefit worth $20/month? Friend recommends it

### Warp Terminal
- [ ] Evaluate Warp as alternative
- Positions itself as "Agentic Development Environment" - has its OWN built-in agent
- NOT a Claude Code host - it's a competitor (though you CAN run Claude Code CLI inside it)
- Supports Claude, GPT-5, Gemini natively
- Agent profiles, global rules, codebase indexing
- **Cost**: Free tier (75 AI credits/month), Build plan $20/month (1500 credits), BYOK supported
- **Gotcha**: AI suggestions burn credits as you type, before even submitting

### Parallel Sessions (Three Tiers)

**Tier 1 - Git worktrees (Anthropic recommended, zero overhead)**
```bash
git worktree add ../project-feature-a -b feature-a
cd ../project-feature-a && claude
```
Each worktree = isolated files, shared git history. One Claude session per worktree.

**Tier 2 - tmux orchestration (community gold standard)**
- tmux windows/panes + git worktrees together
- Session persistence (detach/reattach), visual monitoring
- Tools: [Claudeman](https://github.com/Ark0N/Claudeman) (web UI, up to 20 parallel sessions, token tracking)
- Tools: [crystal](https://github.com/stravu/crystal) (desktop app for parallel worktree sessions)

**Tier 3 - Agent Teams (experimental, built-in)**
- Enable: `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` in settings.json
- One lead + N teammates, each with own context window
- Shared task list + mailbox for inter-agent messaging
- Display: "in-process" (Shift+Down to cycle) or "split-pane" (tmux/iTerm2 only)
- Limitations: no session resumption with teammates, one team per session, no nested teams

### Tools for Parallel Workflows
- [ ] [Claudeman](https://github.com/Ark0N/Claudeman) - Web UI for 20 parallel Claude Code sessions with xterm.js
- [ ] [crystal](https://github.com/stravu/crystal) - Desktop app managing parallel sessions in worktrees
- [ ] [ccpm](https://github.com/automazeio/ccpm) - GitHub Issues + worktrees for spec-driven parallel dev
- [ ] [parallel-worktrees skill](https://github.com/spillwavesolutions/parallel-worktrees) - Claude Code skill for worktree workflow

## 3D & CAD

- [ ] [OpenSCAD](https://openscad.org/) - Programmers' solid 3D CAD modeller

## Notebooks

- [ ] [Google Colab](https://colab.research.google.com/) - Free cloud notebooks
