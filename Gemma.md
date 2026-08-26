# Gemma 

Gemma4 can be used as a local model in a few diffent ways.

---

##  Use Gemma4 through Open WebUI

- 01 Start gemma4 local model with Ollama: `ollama run gemma4`
- 02 Start the Open-WebUI container in Docker and open it @ http://localhost:3000/
- 03 [How to Enable Web Search in Open WebUI Professor Patterns](https://www.youtube.com/watch?v=fwscnJu_Md0)  

Step 03 enables `Open WebUI` to use the `Web Search` feature through a 
search engine service that you can choose and set up.

---

##  Use Gemma4 through Copilot CLI

In a terminal, i.e. a Visual Studio Code terminal use the following
to start a session with the local model gemma4

```
$env:COPILOT_PROVIDER_BASE_URL = "http://localhost:11434/v1"
$env:COPILOT_MODEL = "gemma4:latest"
$env:COPILOT_OFFLINE = "true"
copilot
```

---

# Documentation

[Google AI for Developers: Gemma 4](https://ai.google.dev/gemma/docs/core)  

---

# Articles

[A Visual Guide to Gemma 4 12B](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-gemma-4-12b)  

---

# Videos 

[Gemma 4 12B Is INSANE – Is THIS the BEST Local Coding Model Yet? Bijan Bowen](https://www.youtube.com/watch?v=LJIfSr2fVTc&t=1304s)  

[Gemma 4 makes a surprisingly good local Copilot Telusko](https://www.youtube.com/watch?v=CyiqH3SoqBM)  

[Master Gemma 4 in 20 Minutes  Ali H. Salem](https://www.youtube.com/watch?v=yJr_kTCOkFo)  

[Google Gemma 4 Tutorial - Run AI Locally for Free Teacher's Tech](https://www.youtube.com/watch?v=7LEvSOiTWZk)  

[Gemma 4 Just Got Way More Powerful with Open WebUI Teacher's Tech](https://www.youtube.com/watch?v=aQ1rblXB91U&t=20s)   

[Why Google Just Gave Away Gemma 4 for Free Ali H. Salem](https://www.youtube.com/watch?v=sXgZhGzqPmU)   

---

# FAQ

## How can I allow my local gemma4 model to use the Internet from within GitHub Copilot CLI?

To give your local Gemma 4 model internet access when using it inside the GitHub Copilot CLI, 
**you need to configure two separate components**: 

- allowing the local model to make external web calls via tool calling, and 
- preventing the Copilot CLI from enforcing offline mode

> Step 1: Ensure `COPILOT_OFFLINE` is Disabled

When running local LLM providers (like Ollama or LM Studio) with Copilot CLI, 
the CLI is often executed with `COPILOT_OFFLINE="true"`. Ensure this variable is not set so 
the CLI doesn't block out-of-band requests or tool executions.  

Make sure your shell profile does not set: `export COPILOT_OFFLINE=false  # or leave it unset entirely`

> Step 2: Configure Web Search / Execution Tools for the Local Model

Local models (like Gemma 4 via Ollama or LM Studio) do not natively "browse" the web 
unless given tools (function calls) to execute commands. 

Copilot CLI uses system execution tools to fetch external data (e.g., curl, wget, or terminal web search wrappers).  

1. Verify Tool Calling Support:

Gemma 4 models (such as gemma-4-e2b or larger) support function/tool calling. 
Ensure your local provider exposes an OpenAI-compatible endpoint with function 
calling enabled:  

- LM Studio: Load Gemma 4 and ensure Max Concurrent Predictions is set appropriately (often set to 1 for local stability).  
- Ollama: Serve Gemma 4 using `ollama run gemma4` or `ollama serve`.

2. Configure Copilot CLI Environment Variables:
Point Copilot CLI to your local endpoint:  

```
export COPILOT_PROVIDER_BASE_URL="http://localhost:1234/v1" # or http://localhost:11434/v1 for Ollama
export COPILOT_PROVIDER_TYPE="openai"
export COPILOT_MODEL="google/gemma-4-e2b" # Or your local gemma tag
```

> Step 3: Run Copilot CLI with Tool Permissions Enabled

When using local models, Copilot CLI relies on shell tool invocations (like curl, powershell, or bash) 
to pull live data from the web.  

Launch the Copilot CLI interactively without restricting local executions:  
`copilot --yolo --stream on`

(The `--yolo` flag auto-approves CLI execution tools without prompting for every network/terminal call).

> Step 4: Instruct Gemma 4 to Use Terminal Tools for Web Data

Since local models rely strictly on context and tool parameters, explicitly prompt Gemma 4 
to fetch the target URL or query via terminal tools:  

```
copilot "Use curl to fetch the latest release notes from https://api.github.com/repos/cli/cli/releases/latest and summarize them."
```

### Common Troubleshooting

- Model attempt fails on tool formatting: 

Local models occasionally format JSON tool calls incorrectly. If Gemma 4 fails to format tool calls, 
use a larger quantization variant (e.g., gemma4:26b instead of smaller sub-4B parameters).  

- Context window overflow: 
Ensure you expand the token limit for local web responses by setting:
`export COPILOT_PROVIDER_MAX_PROMPT_TOKENS="65536"`

---

# How do I setup custom MCP web tools or search plugins with local Gemma models in GitHub Copilot CLI?

Which response is more helpful?
Your choice will help Gemini give you more helpful responses. 
Loading the response may take a moment.

---

## Choice A

Setting up Model Context Protocol (MCP) servers in GitHub Copilot CLI 
allows your local Gemma 4 model to execute structured tools like 
real-time web search or API fetching.

Because small or quantized local LLMs can struggle if inundated with 
too many tool definitions, configuring MCP for Gemma 4 requires balancing 
tool search options with strict JSON syntax.

> Step 1: Install a Web Search MCP Server

First, choose an MCP web search server. 
Popular open-source options include: 

- Brave Search MCP (structured web search) 
- Fetch MCP (fetching/converting raw web pages to Markdown)

Install your preferred MCP server globally using npx:

Bash
# Brave Search MCP (requires BRAVE_API_KEY)
`npx -y @modelcontextprotocol/server-brave-search`

# Fetch MCP (fetches and distills web pages, no API key needed)
`npx -y @modelcontextprotocol/server-fetch`

> Step 2: Configure MCP in GitHub Copilot CLI

You can configure MCP servers globally via the `mcp-config.json` file or 
through Copilot CLI's interactive session commands.

> Method A: Interactive Command (Recommended)
Launch your Copilot CLI configured to point to your local Gemma model:

Bash
copilot
In the session prompt, invoke the MCP manager:

Plaintext
/mcp add
Enter a Server Name (e.g., web-search) and select stdio.

Set the command to npx and supply the arguments:

Command: npx

Args: -y @modelcontextprotocol/server-brave-search

> Method B: Manual Configuration File
Edit or create your user-level MCP configuration file at ~/.copilot/mcp-config.json:

```
JSON
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-brave-search"
      ],
      "env": {
        "BRAVE_API_KEY": "YOUR_BRAVE_SEARCH_API_KEY"
      }
    },
    "fetch": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-fetch"
      ]
    }
  }
}
```

> Step 3: Verify Model Support and Context Overhead

Local models process tool definitions directly in their system prompt. 
Gemma 4 handles function calling well, but you should take two key steps 
to optimize performance:

Verify MCP status inside Copilot CLI:

Plaintext
/mcp show

---
## Choice B

Integrating Model Context Protocol (MCP) servers with a local Gemma 4 model in GitHub Copilot CLI 
requires 

- attaching web search plugins via standard MCP configurations, 
- ensuring local provider endpoints support JSON tool calls, 
- and enabling tool access in the CLI.

> Step 1: Add a Web Search MCP Server

You can configure an MCP server using an official web tool package (e.g., `Brave Search or Tavily`)
using the interactive command or by writing the JSON configuration file directly.

- Option A: Interactive Slash Command
Start Copilot CLI and use the `/mcp` command:

Plaintext
copilot
`/mcp add brave-search`
Follow the interactive prompts to define the execution command (npx) and arguments.

- Option B: Manual Configuration (`mcp-config.json`)
Create or edit your local user configuration at `~/.copilot/mcp-config.json`:

```
JSON
{
  "mcpServers": {
    "brave-search": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-brave-search"
      ],
      "env": {
        "BRAVE_API_KEY": "YOUR_BRAVE_SEARCH_API_KEY"
      }
    }
  }
}
```

> Step 2: Configure Environment for Local Gemma 4

Local LLM engines (Ollama, LM Studio) act as the completion provider, while Copilot CLI 
orchestrates tool calls via MCP. 

Configure your local provider to accept function schemas:

Bash

# Point Copilot CLI to local OpenAI-compatible endpoint

```
export COPILOT_PROVIDER_BASE_URL="http://localhost:11434/v1" # Ollama default
export COPILOT_PROVIDER_TYPE="openai"
export COPILOT_MODEL="gemma4:26b" # Quantized model tag with tool capability
```

Note on Model Sizing: Tool calling under MCP relies on precise structural parsing. 
Larger Gemma 4 variants (e.g., gemma4:26b or gemma4:31b) handle MCP tool schemas 
more reliably than smaller 4B quantization formats.

> Step 3: Run Copilot CLI with MCP Tools Enabled
Launch the CLI with explicit tool permissions or auto-execution enabled:

Bash
`copilot --allow-tool="brave-search"`
To view loaded tools during an active session, use the /mcp show slash command.

> Step 4: Execute a Web Search Prompt
Instruct the local Gemma 4 model to fetch live data using the configured MCP tool:

Plaintext
`copilot "Search the web using brave-search for the latest GitHub Copilot CLI patch release notes."`

---

## What is the context windows for Gemma 4?

[Gemma 4 model overview](https://ai.google.dev/gemma/docs/core)  

Gemma 4 released with text, audio and image input and long up to 256K context window,
and maintains multilingual support in over 140 languages.

The small models feature a 128K context window, while the medium models support 256K.

> Long Context 

Context windows of up to 128K tokens (E2B/E4B) and 256K tokens (12B/26B A4B/31B).

---

## Does open webui use ollama?

Yes, Open WebUI uses Ollama as its primary local backend to run large language models.
However, it is not strictly required.Native Integration: Open WebUI is designed to natively connect with Ollama, allowing you to manage models directly from the UI, pull new ones, and view GPU performance.No Ollama Required: You can use Open WebUI without Ollama. 

It also supports other OpenAI-compatible APIs (like Anthropic, OpenAI, or LocalAI). If you run it via Docker, you can disable the Ollama requirement entirely by setting the environment variable -e ENABLE_OLLAMA_API=False.

---

## Use the graphic card with Open WebUi

To use a graphics card with Open WebUI, the GPU isn't meant for the Open WebUI interface itself (which is just a frontend); instead, your GPU needs to be assigned to your backend inference engine, such as Ollama or llama.cpp.Follow these steps to set it up:1. Install the GPU Driver & ToolkitNvidia: Ensure you have your latest proprietary drivers and the NVIDIA Container Toolkit installed so Docker can access your GPU.Intel/AMD: Ensure you have ROCm (AMD) or IPEX-LLM (Intel Arc) installed.2. Run the Backend with GPU SupportYou need to pass the GPU flag to your backend (Ollama) container so it offloads Large Language Model computations to your graphics card.If you are using Docker with Nvidia, run Ollama with GPU support enabled:bashdocker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

Usa il codice con cautela.3. Run Open WebUI with GPU SupportWhile Open WebUI runs fine on a CPU, if you want to use the GPU for advanced local tasks like text-to-speech, audio transcription (Whisper), or document embeddings (for RAG), you should deploy the CUDA version of the Open WebUI container.Run the following command in your terminal:bashdocker run -d -p 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda

Usa il codice con cautela.Note: If you already have Ollama installed natively on Windows/Linux (not inside Docker), you can just run Open WebUI as normal, and it will auto-detect the Ollama instance at localhost:11434.4. Connect and VerifyOpen your browser and go to http://localhost:3000.Create your administrator account and log in.Go to Settings > Connections and ensure your Ollama API URL is set (e.g., http://localhost:11434 or http://docker.internal if Ollama is running in Docker).Go to Models in the panel to download models (e.g., llama3), which will now be processed using your graphics card.

---

# How to set a search engine in Open WebUI?


[How to Enable Web Search in Open WebUI Professor Patterns](https://www.youtube.com/watch?v=fwscnJu_Md0)  

[How to Setup Web Search in Open WebUI with NO APIs! Gray Technical](https://www.youtube.com/watch?v=m_gnqic6u_Q)  

[Web Search - Open WebUI](https://docs.openwebui.com/troubleshooting/web-search/)  

[Browser Search Engine Integration - Open WebUI](https://docs.openwebui.com/tutorials/integrations/dev-tools/browser-search-engine/)  

---

## Google Programmable Search Engine (PSE)

[Google Programmable Search Engine (PSE) - Docs](https://docs.litellm.ai/docs/search/google_pse)   
[Google Programmable Search Engine (PSE)](https://programmablesearchengine.google.com/about/)  
[google discontinuing "entire web" search #107](https://github.com/zoharbabin/google-researcher-mcp/issues/107)  

[Google Custom Search Engine (CSE) alternative, built on Elasticsearch](https://www.elastic.co/fr/google-custom-search-engine-alternative)  

*.com, *.co.uk, *.net, *.co, *.io, *.ai, *.de, *.it

---

# How can I let Gemma 4 access the internet when I use it with Ollama and Open WebUI?

To give Gemma 4 internet access, enable the built-in web search feature in Open WebUI. 

Open WebUI handles the internet search via a search engine provider and injects the 
live results directly into your local Gemma 4 chat context.

## Configure Web Search in Open WebUI

1. Click your profile icon in the bottom-left corner of Open WebUI and open the Admin Panel.

2. Go to Settings and select Web Search.

3. Toggle Enable Web Search to active.

4. Choose a Web Search Engine from the dropdown list (such as DuckDuckGo, SearXNG, Google PSE, or SearchAPI).

5. Fill in any required fields or API keys for your chosen provider (DuckDuckGo or a self-hosted SearXNG often require no paid key), then click Save.

## Use Internet Search in Chat

- Activate per query: 

In the chat prompt box, click the search/plus button or toggle the web search option on 
before sending your message so Gemma 4 can pull live web context.

- Adjust context length: 

Ensure your model's context window in Open WebUI is set high enough 
(e.g., 8192 or 16384 tokens instead of the default 2048) so Gemma 4 has enough memory 
to read and process the injected web search data.

---

# Can Gemma 4 access the internet?

By itself, Gemma 4 is an open-weights on-device model that runs completely offline. 
It cannot natively access the internet on its own, but it can use the internet if the 
software platform, app, or developer harness running it provides a web-search tool or 
API integration.

## How Gemma 4 Handles Connectivity

- Offline Functionality: 

Once downloaded (via apps like the Google AI Edge Gallery or platforms like Ollama),
Gemma 4 operates 100% locally on your phone, tablet, or computer without any internet 
connection or cellular signal.

- Using External Tools: 

The model itself is just text-in, text-out. 
If it is integrated into a development environment (such as Android Studio) or a chat 
interface with web-search capabilities, the surrounding software harness—not the model 
file itself—handles fetching data or making API calls from the internet.

- Community Consensus: 

Users on Reddit generally agree that any web-browsing or live-data retrieval behavior 
depends entirely on whether you have paired the model with an external tool or search plugin.

---

# Are you (Gemma4) able to access the Internet to find relevant information when I ask you a question?

As a large language model, I do not have the ability to browse the live, 
real-time internet like a web browser does. My knowledge comes from the 
vast dataset I was trained on, and that dataset has a specific cutoff date, 
meaning I cannot provide information about events that happened after my 
last update.

However, I *can* assist you with information from several sources if they 
are available to me through our current chat context and the tools provided:

1.  **Internal Knowledge Bases:** 

I can search and analyze specific knowledge bases, documents, and files that 
you have access to (using tools like `query_knowledge_bases` or `query_knowledge_files`).

2.  **Saved Information:** 
I can search your personal saved memories, notes, and past chat history.

3.  **Calendar/Tasks:** 
I can retrieve or manage your scheduled events and tasks.

So, while I can't give you breaking news or check live websites, I am very 
powerful at synthesizing, analyzing, and retrieving information from defined, 
internal sources.

---

# How many parameters has gemma 4?

[gemma4](https://ollama.com/library/gemma4/tags)  

Google's Gemma 4 is not a single model, but a family of open-weight models 
with varying parameter sizes ranging from roughly 2 billion up to 31 billion 
parameters.

## Gemma 4 Model Sizes

- Gemma 4 E2B: 
~2.3 billion effective parameters (around 5.1B including per-layer embedding tables)

- Gemma 4 E4B: 
~4.5 billion effective parameters (around 8B including embeddings)

- Gemma 4 12B Unified: 
~12 billion dense parameters (encoder-free architecture)Gemma 4 26B A4B: 26 billion total parameters in a Mixture-of-Experts (MoE) setup, with about 3.8B to 4B parameters active per token during inference

- Gemma 4 31B: 
31 billion parameters in a standard dense configuration

## This is the output of  `ollama ls ` on my PC which one of the gemma4 version is installed on my machine?

Use ` ollama ls` to get a list of locally installed models:

```
NAME             ID              SIZE      MODIFIED     
gemma4:latest    c6eb396dbd59    9.6 GB    2 months ago 
```

Based on the file size of 9.6 GB and the `c6eb396dbd59` ID from your ollama ls output, 
you have the `Gemma 4 E4B` version installed on your machine.

---