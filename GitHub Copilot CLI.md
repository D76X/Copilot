# GitHub Copilot CLI

[GitHub Copilot CLI command reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)   

Use `copilot` in front of all the follwoing.

| Command           | Effect    | Description | Notes |
| :---------------- | :-------: | ----------------------------------------------: | ----: |
| login             | Init      | Authenticate with Copilot via the OAuth device flow. | `copilot login` |  
| mcp               | Conf      | Manage MCP server configurations from the command line. | `copilot mcp` |  
| help providers    | Help      | show the help for the `providers` command | `copilot help providers` |  
| usage             | Usage     | Display session usage metrics and statistics, including per-model token totals. |
| compact           | Usage     | Compaction is the process that allows GitHub Copilot CLI to support long-running sessions without hitting the limits of the context window. |

---

[Slash commands in the interactive interface](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference#slash-commands-in-the-interactive-interface)  

| Command           | Effect    | Description | Notes |
| :---------------- | :-------: | ----------------------------------------------: | ----: |
| /research TOPIC   | ...       | Run a deep research investigation using GitHub search and web sources. 
See Researching with GitHub Copilot CLI.. | it generates a report. It can be used beside any MCP servers. |  

---

## Context Windows Usage and Optimization

[Compaction](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/context-management#compaction)   
[Checking your context usage](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/context-management#checking-your-context-usage)   

| Command           | Effect    | Description | Notes |
| :---------------- | :-------: | ----------------------------------------------: | ----: |
| usage             | Usage     | Display session usage metrics and statistics, including per-model token totals. |
| compact           | Usage     | Compaction is the process that allows GitHub Copilot CLI to support long-running sessions without hitting the limits of the context window. |

---


### Copilot

Here's a clear breakdown of these two commands and how they work together:

---

## `/agent` — *Who* handles your task

`/agent` selects a **specialized Copilot persona** with a specific role, toolset, and behavior:

| Agent | Best for |
|---|---|
| **Explore** | Quick codebase Q&A without polluting main context |
| **General Purpose** | Complex multi-step tasks, high-quality reasoning |
| **Task** | Running builds, tests, shell commands |
| **Code Review** | Surfacing real bugs, ignoring noise |
| **Research** | Deep investigation across code, repos, and web |
| **Rubber Duck** | Critical feedback on your implementation |

You switch with `/agent <name>` or just say _"Use the research agent to..."_ in your prompt.

---

## `/model` — *What brain* powers the agent

`/model` selects the **underlying AI model** (e.g., Claude Sonnet, Claude Opus, GPT-5). It's orthogonal to agent — same agent, different reasoning power.

Key variants:
- `/model auto` — let Copilot pick optimally
- `/model <name> --repo` — set a repo-wide default
- `/model <name> --plan` — set the model specifically for **plan mode**

You can also configure **per-agent models** with `/subagents` — so subagents can use a different (often lighter/cheaper) model than your main session.

---

# What can the commands /agent and /model do taken together?

my colleague suggested to use the GitHub copilot /agent and set the agent and I know 
that I can use the command /model to pick the model to work with within a copilot session. 
However, I do not really know and understand the relation ship between these two command 
and what they are used for induvidually and also taken together and how I could use them 
to improve my copilot workflow according to teh task at hand. Plkease, educate me on the subject.


## Together: Match agent + model to your task

| Task | Agent | Model strategy |
|---|---|---|
| Deep architectural investigation | Research / General Purpose | Powerful model (Opus/GPT-5) |
| Quick "what does this file do?" | Explore | Lighter/faster model |
| Running CI, builds, tests | Task | Lighter model is fine |
| Complex refactor or new feature | General Purpose | Powerful model |
| PR review before merge | Code Review | Powerful model |
| Planning a big change | Plan mode (`Shift+Tab`) | Set dedicated model via `/model --plan` |


**Bottom line:** 

Think of `/agent` as choosing a specialist colleague, and `/model` as 
choosing how sharp their thinking is. For routine or mechanical tasks, 
a lighter model + task agent saves resources. For high-stakes reasoning, 
a powerful model + general-purpose or research agent gives the best results.

---

