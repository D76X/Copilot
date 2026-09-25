#  OpenCode

[OpenCode - The open source AI coding agent](https://gemini.google.com/app/bc1b6b997acc78fb?utm_source=app_launcher&utm_medium=owned&utm_campaign=base_all)  

---

# What is OpenCode?

**OpenCode** is an open-source, model-agnostic AI coding agent designed primarily for terminal-first development. It connects directly to your workspace, local files, and 
development tools to automate programming tasks such as writing code, fixing bugs, 
running tests, and managing Git workflows.

Unlike single-vendor solutions (like Anthropic's Claude Code or GitHub Copilot), OpenCode operates as an open ecosystem framework under the MIT license.

---

### Key Features

* **Model Agnostic:** Works with over 75 model providers. You can route requests to Anthropic (Claude), OpenAI (GPT-4 / GPT-5), Google (Gemini), or run completely offline using local models via Ollama or LM Studio.

* **LSP Integration:** Connects with the Language Server Protocol (LSP). When OpenCode makes a change, it reads real-time compiler and linter diagnostics to self-correct syntax or type errors automatically.

* **Agentic Tool Execution:** Can search files (`grep`/`glob`), read and edit source code, and run shell commands in the terminal.

* **Git-Based Snapshots (`/undo` & `/redo`):** Takes snapshots of your workspace prior to applying edits, making it simple to revert changes if an agentic plan misses the mark.

* **MCP Support:** Implements the Model Context Protocol (MCP) to seamlessly connect to external tools, databases, and APIs.

* **Client-Server Architecture:** Runs a local server that powers a Terminal User Interface (TUI), desktop app, IDE extensions, or remote CLI clients.

---

### How it Works

OpenCode operates in two main modes:

1. **Build Mode (Default):** The agent autonomously reads files, writes code, and runs terminal commands.

2. **Plan Mode:** The agent acts as an advisor—it analyzes the codebase and drafts execution plans, but asks for explicit confirmation before editing files or executing shell scripts.

Configurations and custom project instructions are managed in plain files (such as `AGENTS.md` or `.opencode.json`), allowing teams to check in project-specific agent behaviors directly into version control.

---