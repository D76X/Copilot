# Give local Gemma 4 web search through Open WebUI

This guide connects the already-installed `gemma4:latest` Ollama model to
Open WebUI's web-search tool on this Windows PC. Gemma itself remains local:
Open WebUI performs the network requests, retrieves relevant page content, and
supplies that content to Gemma as chat context.

## What you need

- Ollama running on Windows with `gemma4:latest` installed.
- Docker Desktop running, if Open WebUI is installed in Docker.
- An Open WebUI administrator account.

The model does **not** receive unrestricted Internet access, and it needs no
network-specific Ollama configuration. It can only use the web-search tool that
Open WebUI exposes and that the chat/model configuration permits.

## 1. Start the existing services

1. Start **Docker Desktop** and wait until it reports that its engine is
   running. Docker was not running when this guide was prepared, so an existing
   Open WebUI container cannot start until this step is complete.
2. In PowerShell, confirm that Ollama exposes the installed model:

   ```powershell
   curl.exe http://localhost:11434/api/tags
   ```

   The JSON response should include `gemma4:latest`.
3. If Open WebUI has an existing container, start it without deleting its
   persistent data:

   ```powershell
   docker start open-webui
   ```

   If its name is different, find it first:

   ```powershell
   docker ps -a --format "table {{.Names}}`t{{.Status}}"
   ```

4. Open <http://localhost:3000> and select `gemma4:latest` in a new chat.

If Open WebUI cannot list the model, open its administrator settings and set
the Ollama base URL to `http://host.docker.internal:11434`. This hostname is
important when Open WebUI runs in Docker: `localhost` inside the container
means the container, not this Windows host.

---

## 2. Recommended first setup: DuckDuckGo

DuckDuckGo is the fastest way to confirm the feature because it needs no API
key or extra service. Searches are still sent to DuckDuckGo, so use the
SearXNG option below if keeping query traffic local is important.

1. In Open WebUI, open **Admin Panel** and find **Settings > Web Search**.
   Depending on the installed Open WebUI version, this section may appear
   under **Retrieval**.
2. Turn on **Enable Web Search**.
3. Select **DuckDuckGo** (shown as `duckduckgo` or `ddgs` in some versions) as
   the search engine, then save.
4. Open the Gemma model's advanced settings. Enable **Web Search** and set
   **Function Calling** to **Native** when those model-level settings are
   available.
5. In a new Gemma chat, switch on the **Web Search** globe/tool control beside
   the prompt. All three gates must be enabled: the global setting, the
   model setting, and the per-chat control.
6. start ollama with the gemma4 local LLM from a terminal: `ollama run gemma4`
7. Ask a time-sensitive question, for example:

   ```text
   Search the web for the current Open WebUI release and give me its version,
   release date, and source links.
   ```

   A successful response includes source citations. Do not accept an
   uncited answer as proof that live search worked.

---

## 3. Private no-key option: self-host SearXNG

Choose this option when you prefer a local metasearch service or DuckDuckGo
begins to rate-limit frequent searches. SearXNG still queries the upstream
engines it is configured to use; it does not make external search results
magically local.

The official SearXNG Compose template is the safest starting point. 
In PowerShell:

```powershell
New-Item -ItemType Directory -Force "$HOME\searxng\core-config" | Out-Null
Set-Location "$HOME\searxng"
curl.exe -fsSLO https://raw.githubusercontent.com/searxng/searxng/master/container/docker-compose.yml
curl.exe -fsSLO https://raw.githubusercontent.com/searxng/searxng/master/container/.env.example
Copy-Item .env.example .env
notepad .env
```

Set the host port in `.env` to `8888` if the template exposes a port setting.
Then start the service:

```powershell
docker compose up -d
docker compose ps
```

Edit `$HOME\searxng\core-config\settings.yml` and ensure its `search` section
allows the JSON output that Open WebUI requires:

```yaml
search:
  formats:
    - html
    - json
```

Restart after saving:

```powershell
docker compose restart
curl.exe "http://localhost:8888/search?q=Open+WebUI&format=json"
```

The last command must return JSON with a `results` array. A `403 Forbidden`
response usually means that `json` was not enabled or SearXNG was not
restarted.

Back in Open WebUI's **Admin Panel > Settings > Web Search**:

1. Select **SearXNG** as the engine.
2. Set the query URL to
   `http://host.docker.internal:8888/search`.
3. Save, enable web search for Gemma and the chat as in step 2, then repeat
   the cited search test.

Use `host.docker.internal` because Open WebUI needs to reach a service on the
Windows host. If Open WebUI and SearXNG instead share one Docker Compose
network, use SearXNG's Compose service name and its container port rather than
this host address.

---

## 4. Use local Gemma 4 through Copilot CLI

Copilot CLI can use the same local Ollama model through its BYOK (bring your
own model) support. This is a separate path from Open WebUI: Open WebUI's
search toggle and SearXNG configuration do not automatically carry over to
Copilot CLI.

Before starting Copilot CLI, confirm that Ollama's OpenAI-compatible endpoint
can list the model:

```powershell
curl.exe http://localhost:11434/v1/models
```

Then start a **new PowerShell session** and configure the provider:

```powershell
$env:COPILOT_PROVIDER_TYPE = "openai"
$env:COPILOT_PROVIDER_BASE_URL = "http://localhost:11434/v1"
$env:COPILOT_MODEL = "gemma4:latest"
$env:COPILOT_OFFLINE = "true"
copilot
```

`openai` is the correct provider type for Ollama's OpenAI-compatible endpoint.
No API key is needed for a default local Ollama installation. `COPILOT_OFFLINE`
prevents Copilot CLI from contacting GitHub services; it does **not** give
Gemma web search and should not be treated as a general Internet firewall.

Copilot CLI requires the provider model to support both streaming and tool
(function) calling. If startup or tool use fails, update Ollama and verify that
the installed Gemma variant has those capabilities. A local model will also
generally be less reliable at tool calls than a larger, purpose-trained coding
model.

### Retrieve a known public URL

Copilot CLI can ask permission to run PowerShell commands. For a known URL,
this is the simplest, key-free way to provide live content to local Gemma:

```text
Use PowerShell Invoke-WebRequest to retrieve the official Ollama release notes
at https://github.com/ollama/ollama/releases, then summarize the newest release
and link to the source. Ask for approval before running the command.
```

Review the proposed command before approving it. The fetched page content is
sent to the local Ollama endpoint as part of the tool result. Because the model
and Ollama are local, it is not sent to GitHub when offline mode is enabled,
but the requested URL is still contacted over the Internet.

### Add query-based search with an MCP server

For searches such as "find recent articles about X", add an MCP server from a
search provider you trust. MCP is the mechanism by which Copilot CLI obtains
additional structured tools; it is not installed automatically. A search
provider may require an account or API key, and its privacy policy determines
where searches and retrieved content are sent.

For a remote HTTP MCP server, use the endpoint and authentication method in the
provider's own documentation:

```powershell
copilot mcp add --transport http <server-name> <provider-mcp-url>
copilot mcp list
```

For a local `stdio` MCP server, installed according to that server's
documentation, use:

```powershell
copilot mcp add <server-name> -- <command> <arguments>
copilot mcp list
```

If the provider requires a secret, pass it through the command's `--header` or
`--env` option rather than writing it into a repository file. Start a new
`copilot` session after adding the server, then ask Gemma to use the named
search tool and require source links in its answer.

SearXNG itself provides a search HTTP API but is not an MCP server. It can
continue to power Open WebUI as described above; to expose it to Copilot CLI,
use an MCP adapter that you have reviewed and configured specifically for
SearXNG.

### Choose the right path

| Need | Recommended path |
| --- | --- |
| General web-assisted chat with minimal setup | Open WebUI plus DuckDuckGo |
| Local metasearch service and Open WebUI | Open WebUI plus SearXNG |
| Read and summarize a known official URL while coding | Copilot CLI plus an approved PowerShell retrieval command |
| Search from Copilot CLI by topic or keywords | Copilot CLI plus a trusted search-provider MCP server |

## 5. Keep retrieved pages within Gemma's context

Web pages are much larger than ordinary prompts. In Open WebUI, set Gemma's
**Advanced Params** context length to at least `16384` when memory permits.
Keep the web-search result count at `3` initially. Increase it only after
searches work consistently; more results increase latency, memory use, and the
chance of irrelevant context.

For an Ollama-only context change, create a derived model rather than changing
the downloaded model:

```text
FROM gemma4:latest
PARAMETER num_ctx 16384
```

Save this as `Modelfile`, then run:

```powershell
ollama create gemma4-web -f .\Modelfile
```

Select `gemma4-web` in Open WebUI. Do this only if the Open WebUI model setting
does not already provide the needed context length.

## Troubleshooting

| Symptom | Likely cause and correction |
| --- | --- |
| Open WebUI cannot see Gemma | Confirm `curl.exe http://localhost:11434/api/tags`; for a Dockerized Open WebUI use `http://host.docker.internal:11434`, not `localhost`. |
| Search toggle is available but Gemma answers from memory | Enable web search globally, on the model, and in the active chat. Confirm Native function calling is enabled. Smaller models can still fail to issue a structured tool call. |
| SearXNG returns 403 | Add `json` under `search.formats` in `settings.yml`, then restart SearXNG. |
| Sources are empty or pages fail to load | Increase model context; reduce result count; check logs with `docker logs open-webui --tail 50`. For an organisation proxy, enable **Trust Proxy Environment** in Open WebUI web-search settings. |
| Docker commands fail before they run | Start Docker Desktop and wait for its Linux engine to become available. |

## References

- [Open WebUI: Quick Start with Docker](https://docs.openwebui.com/getting-started/quick-start/)
- [Open WebUI: Web Search troubleshooting](https://docs.openwebui.com/troubleshooting/web-search/)
- [SearXNG: Docker installation](https://docs.searxng.org/admin/installation-docker.html)
- [Ollama API introduction](https://docs.ollama.com/api/introduction)
- [GitHub Copilot CLI: Using your own LLM models](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/use-byok-models)
- [GitHub Copilot CLI: MCP command reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)
- [How to Enable Web Search in Open WebUI (Professor Patterns)](https://www.youtube.com/watch?v=fwscnJu_Md0)
- [How to Setup Web Search in Open WebUI with No APIs (Gray Technical)](https://www.youtube.com/watch?v=m_gnqic6u_Q)

Tutorial interfaces can age quickly. Prefer the Open WebUI troubleshooting
guide above when a video shows a different settings path or an obsolete URL
format.
