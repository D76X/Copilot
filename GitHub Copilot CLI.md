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

## How can I use a local model when I use GitHub Copilot CLI? 

[Using your own LLM models in GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/use-byok-models#configuring-your-provider)  

[GitHub Copilot > Configuring your provider](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/use-byok-models#configuring-your-provider)  

| Environment Variable | Required / Optional | Meaning |
| :--- | :--- | :--- |
| `COPILOT_PROVIDER_BASE_URL` | Required | The base URL of your model provider's API endpoint. |
| `COPILOT_MODEL` | Required | The model identifier to use. You can also set this with the `--model` command-line flag. |
| `COPILOT_PROVIDER_TYPE` | Optional | The provider type: openai (default), azure, or anthropic. |
| `COPILOT_PROVIDER_API_KEY` | Optional | Your API key for the provider. Not required for providers that do not use authentication, such as a local Ollama instance. |

> Example 01:

```
$env:COPILOT_PROVIDER_BASE_URL = "http://localhost:11434/v1"
$env:COPILOT_MODEL = "gemma4:latest"
$env:COPILOT_OFFLINE = "true"

copilot

am I using the gemma4:latest local model in this GtiHub Copilot session?

I'm powered by gemma4:latest (model ID: gemma4:latest).
The model is hosted via your Copilot session environment and acts as my backbone. I do not operate strictly as a local, self-contained application but rather as an Assistant service integrated into the terminal workflow using this specified model architecture.

```

> Notes:

The `v1` at the end of "http://localhost:11434/v1" is necessary.
Ollamma itself runs as backend at "http://localhost:11434" but the API endpoint is the `v1`.

---

> `copilot help providers`

---

```
Custom Model Providers (BYOK):

  Use your own model provider instead of GitHub Copilot's model routing.
  Set the COPILOT_PROVIDER_BASE_URL environment variable to activate BYOK mode.
  GitHub authentication is not required when using a custom provider.

Environment Variables:

  COPILOT_PROVIDER_BASE_URL          API endpoint URL (required to activate BYOK)
  COPILOT_PROVIDER_TYPE              "openai" (default), "azure", or "anthropic"
  COPILOT_PROVIDER_API_KEY           API key (optional for local providers like Ollama)
  COPILOT_PROVIDER_BEARER_TOKEN      Bearer token (takes precedence over API key)
  COPILOT_PROVIDER_WIRE_API          "completions" (default) or "responses"
  COPILOT_PROVIDER_TRANSPORT         "http" (default) or "websockets"
  COPILOT_PROVIDER_AZURE_API_VERSION Azure API version (default: versionless v1)

Model Configuration:

  COPILOT_MODEL                             Model name (sets both model ID and wire model)
  COPILOT_PROVIDER_MODEL_ID                 Well-known model ID for agent config and token limits
  COPILOT_PROVIDER_WIRE_MODEL               Model name sent to the provider API for inference
  COPILOT_PROVIDER_MAX_PROMPT_TOKENS        Maximum prompt tokens
  COPILOT_PROVIDER_MAX_OUTPUT_TOKENS        Maximum output tokens

  A model is required for BYOK. Set COPILOT_MODEL, COPILOT_PROVIDER_MODEL_ID, or --model.

  COPILOT_MODEL is the simplest option: it sets both the model ID (used internally for
  agent configuration and token limits) and the wire model (sent to the provider).

  When the wire model differs from the base model (e.g., a fine-tuned variant or
  Azure deployment), set COPILOT_PROVIDER_MODEL_ID to a well-known base model name
  (like "gpt-5.4" or "claude-sonnet-4") and COPILOT_PROVIDER_WIRE_MODEL to the
  name your provider expects. Matching a well-known model ID lets the agent use
  model-specific configuration such as tool support, token limits, and prompting
  strategies. Without a recognized model ID, the agent falls back to safe defaults.
  Both default to COPILOT_MODEL when not set explicitly.

  Token limits are resolved in order: manual env vars → built-in model catalog → defaults.

  Use "openai" type for any OpenAI-compatible endpoint, including Ollama, vLLM,
  and Foundry Local. Use "responses" wire API for GPT-5 series models.
  Add COPILOT_PROVIDER_TRANSPORT=websockets to use websockets for the responses API.

Examples:

  # Ollama (local, no API key required)
  $ COPILOT_PROVIDER_BASE_URL=http://localhost:11434/v1 \
    COPILOT_MODEL=deepseek-coder-v2:16b \
    copilot

  # Custom OpenAI-compatible endpoint
  $ COPILOT_PROVIDER_BASE_URL=https://my-api.example.com/v1 \
    COPILOT_PROVIDER_API_KEY=sk-... \
    COPILOT_MODEL=gpt-4 \
    copilot

  # Azure OpenAI with a custom wire model
  $ COPILOT_PROVIDER_TYPE=azure \
    COPILOT_PROVIDER_BASE_URL=https://my-resource.openai.azure.com \
    COPILOT_PROVIDER_API_KEY=your-key-here \
    COPILOT_PROVIDER_MODEL_ID=gpt-4 \
    COPILOT_PROVIDER_WIRE_MODEL=my-gpt4-deployment \
    copilot

  # Anthropic
  $ COPILOT_PROVIDER_TYPE=anthropic \
    COPILOT_PROVIDER_BASE_URL=https://api.anthropic.com \
    COPILOT_PROVIDER_API_KEY=sk-ant-... \
    COPILOT_MODEL=claude-sonnet-4-20250514 \
    copilot

Notes:
  - For Azure endpoints, use type "azure" (not "openai") and provide only the
    host URL (e.g., https://my-resource.openai.azure.com). The SDK constructs
    the full path automatically.
  - See `copilot help environment` for quick reference of all environment variables.
```

---

> Exaple-02

```
$env:COPILOT_PROVIDER_TYPE = "openai"
$env:COPILOT_PROVIDER_BASE_URL = "http://localhost:11434/v1"
$env:COPILOT_PROVIDER_API_KEY = "ollama"
$env:COPILOT_MODEL = "qwen3.5"
$env:COPILOT_OFFLINE = "true"
copilot
```

---

### Videos

[Use ANY AI Model with GitHub Copilot Kayla Cinnamon](https://www.youtube.com/watch?v=bbIHmbZux8k)  

### Articles

[Copilot CLI now supports BYOK and local models](https://github.blog/changelog/2026-04-07-copilot-cli-now-supports-byok-and-local-models/#:~:text=GitHub%20Copilot%20CLI%20now%20lets,using%20GitHub%2Dhosted%20model%20routing.)  

### Documentation

[Running in offline mode](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/use-byok-models#running-in-offline-mode)  

---
