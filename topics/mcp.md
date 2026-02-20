# MCP (Model Context Protocol)

Specs, tutorials, servers, and tooling for MCP.

## Core Docs

- [ ] [MCP Introduction](https://modelcontextprotocol.io/introduction) - Official spec intro
- [ ] [Building MCP with LLMs](https://modelcontextprotocol.io/tutorials/building-mcp-with-llms) - Tutorial
- [ ] [Code Execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp) - Anthropic engineering blog

## Registries & Servers

- [ ] [MCP Registry](https://github.com/mcp) - Official GitHub registry
- [ ] [Best MCP Servers List](https://mcp-server-list.com/) - Community curated list
- [ ] [Serena](https://github.com/oraios/serena) - Semantic retrieval & editing MCP server (+ Agno integration)

## To Configure

- [ ] **NotebookLM MCP** - Set up and connect the NotebookLM MCP server to Claude Code. Would enable querying NotebookLM sources/notebooks directly from the CLI.
- [ ] **[Obsidian](https://obsidian.md/)** - Research whether Obsidian is the right tool for organizing this "second brain." Markdown-based, local-first, plugin ecosystem, graph view for connections. Potential future integration with OpenClaw. Needs a research deep-dive to evaluate fit.

## Research Topics

- [ ] Progressive tool discovery — `defer_loading` for 20-100 tools, code execution for 100+. Key insight: skip MCP entirely for less than 20 tools, use direct Python recipes instead.
- [ ] Direct-code execution pattern — Agent writes Python that calls libraries directly via Bash instead of MCP protocol. 98.7% token savings vs MCP. Pattern at ~/cc_agents/recipes/_PATTERN.md
- [ ] Tool use examples — JSON schema + input_examples for 72%→90% accuracy on complex parameter handling
