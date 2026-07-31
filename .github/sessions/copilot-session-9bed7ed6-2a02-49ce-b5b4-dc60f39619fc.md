# Copilot CLI Session

> [!NOTE]
> - **Session ID:** `9bed7ed6-2a02-49ce-b5b4-dc60f39619fc`  
> - **Started:** 7/29/2026, 4:38:22 PM  
> - **Duration:** 1315m 28s  
> - **Exported:** 7/30/2026, 2:33:51 PM  

---

<sub>1m 30s</sub>

### Info

Model changed from gpt-5.6-sol (medium) to Auto

---

<sub>4m 17s</sub>

### User

my colleague suggested to use the GitHub copilot /agent and set the agent and I know that I can use the command /model to pick the model to work with within a copilot session. However, I do not really know and understand the relation ship between these two command and what they are used for induvidually and also taken together and how I could use them to improve my copilot workflow according to teh task at hand. Plkease, educate me on the subject.

---

<sub>4m 21s</sub>

### `fetch_copilot_cli_documentation`

<details>
<summary>Arguments</summary>

```json
{}
```

</details>

<details>
<summary>123 lines</summary>

```
# GitHub Copilot CLI Documentation

## README
[Could not load README: Error: ENOENT: no such file or directory, open 'C:\Users\pb00270\.copilot\pkg\win32-x64\1.0.75\README.md']

## Help Command Output
Global
  /help - show full help
  ? - show quick help
  / - commands
  @ - mention files
  # - mention issues and pull requests
  ! - execute shell command
  shift+tab - switch modes
  ctrl+s - stash/pop current prompt
  ctrl+q - enqueue prompt
  ctrl+r - reverse search history
  ctrl+o - toggle all timeline
  ctrl+c - cancel
  ctrl+c×2 - exit
  esc esc - clear input, interrupt, stop agents, or rewind
  ctrl+d - shutdown
  ctrl+z - suspend
  ctrl+l - clear screen
  ctrl+t - toggle reasoning display
  ctrl+x → b - move current task to background
  ctrl+x → o - open most recent link

Input
  ctrl+a - go to line start
  ctrl+e - go to line end
  ctrl+h - delete previous character
  ctrl+w - delete previous word
  ctrl+u - delete from cursor to beginning of line
  ctrl+k - delete from cursor to end of line
  meta+←/→ - move cursor by word
  shift+enter - insert newline
  ctrl+g - edit prompt in $EDITOR

Agent Environment
  /init - Initialize Copilot instructions for this repository
  /agent - Browse and select agents: /agent [name]
  /skills - Manage skills for enhanced capabilities
  /mcp - Manage MCP server configuration
  /plugin - Manage plugins and plugin marketplaces

Agents / Subagents
  /model - Select AI model to use (use 'auto' to let Copilot pick automatically). Use '--repo'/'--local' to set the repo default, or 'plan'/'--plan' to set the plan-mode model.
  /delegate - Send this session to GitHub and Copilot will create a PR; use --base to choose the PR target branch
  /fleet - Enable fleet mode for parallel subagent execution
  /autopilot - Toggle autopilot mode
  /tasks - View and manage tasks (subagents and shell commands)

Code
  /ide - Connect to an IDE workspace
  /diff - Review the changes made in the current directory
  /pr - Operate on pull requests for the current branch
  /review - Run code review agent to analyze changes
  /security-review - Analyze staged and unstaged changes for security vulnerabilities.
  /rubber-duck - Get an independent critique of your current work from the rubber duck agent
  /lsp - Manage language server configuration
  /terminal-setup - Configure terminal for multiline input support (shift+enter)

Permissions
  /allow-all - Enable all permissions (tools, paths, and URLs)
  /add-dir - Add a directory to the allowed list for file access
  /list-dirs - Display all allowed directories for file access
  /cwd - Change working directory or show current directory
  /reset-allowed-tools - Reset the list of allowed tools

Session
  /resume - Switch to a different session (optionally specify session ID, task ID, or name)
  /rename - Rename the current session, or auto-generate a name from conversation
  /context - Show context window token usage and visualization
  /usage - Display session usage metrics and statistics
  /session - View and manage sessions. Use subcommands for details.
  /compact - Summarize conversation history to reduce context window usage. Optionally provide focus instructions.
  /share - Share session or research report to a markdown file, HTML file, GitHub gist, or a shareable GitHub link
  /remote - Toggle remote control from GitHub web and mobile
  /copy - Copy the last response to the clipboard
  /rewind - Rewind the last turn and revert file changes

Help
  /help - Show help for interactive commands
  /changelog - Display changelog for CLI versions. Add 'summarize' to get an AI summary.
  /feedback - Provide feedback about the CLI
  /diagnose - Analyze the current session log, optionally with a custom prompt
  /theme - View or set color mode
  /statusline - Configure status line items
  /footer - Configure status line items
  /update - Update the CLI to the latest version
  /version - Display version information and check for updates
  /experimental - Show available experimental features, or enable/disable experimental mode
  /memory - Show memory status, or enable/disable memory across sessions
  /clear - Abandon this session and start fresh
  /instructions - View and toggle custom instruction files
  /app - Prefer a visual workspace? Try out the GitHub Copilot desktop app

Other commands
  /ask - Ask a quick side question without adding to conversation history
  /chronicle - Session history tools and insights
  /env - Show loaded environment details (instructions, MCP servers, skills, agents, hooks, plugins, LSPs, extensions)
  /exit - Exit the CLI; use 'print' to print the session after exiting alt screen
  /keep-alive - Manage keep-alive mode (prevents system sleep).
  /limits - View or edit session limits; the AI Credit limit is a soft cap
  /login - Log in to Copilot
  /logout - Log out of an OAuth login session
  /new - Start a new conversation
  /plan - Create an implementation plan before coding
  /refine - Rewrite a rough, stream-of-consciousness prompt into a clear one for review (Ctrl+X / then /refine cleans up your current input)
  /research - Run deep research investigation using GitHub search and web sources
  /restart - Restart the CLI, preserving the current session
  /search - Search the conversation timeline
  /settings - Open the settings UI, show, set, or unset a single value ('/settings unset <key>' removes it). Use '--repo'/'--local' to target repo settings.
  /subagents - Configure default and per-agent subagent models
  /user - Manage GitHub user list
  /voice - Manage voice mode (dictation transcription via Foundry Local)

Copilot respects instructions from these locations:
  CLAUDE.md (in git root & cwd)
  GEMINI.md (in git root & cwd)
  AGENTS.md (in git root & cwd)
  .github/instructions/**/*.instructions.md (in git root & cwd)
  .github/copilot-instructions.md (in git root & cwd)
  $HOME/.copilot/copilot-instructions.md
  $HOME/.copilot/instructions/**/*.instructions.md
  COPILOT_CUSTOM_INSTRUCTIONS_DIRS (additional directories via env var)

To learn about what I can do
  Ask me: "What can you do?"
  Or visit: https://docs.github.com/copilot/how-tos/use-copilot-agents/use-copilot-cli

---

**Note**: If the above documentation doesn't answer the user's request, you can fetch additional documentation from the official GitHub Docs for more information.

Use the web_fetch tool to fetch https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli

You can also follow hyperlinks to related docs pages using the same API pattern.
```

</details>


---

<sub>4m 26s</sub>

### `web_fetch`

**https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli**

<details>
<summary>Arguments</summary>

```json
{
  "url": "https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli",
  "max_length": 8000
}
```

</details>

<details>
<summary>92 lines</summary>

````
Contents of https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli:
# Using GitHub Copilot CLI

Learn how to use GitHub Copilot from the command line.

The command-line interface (CLI) for GitHub Copilot allows you to use Copilot directly from your terminal. For more information, see [About GitHub Copilot CLI](/en/copilot/concepts/agents/copilot-cli/about-copilot-cli).

## Prerequisite

Install Copilot CLI. See [Installing GitHub Copilot CLI](/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli).

## Using Copilot CLI

1. In your terminal, navigate to a folder that contains code you want to work with.

2. Enter `copilot` to start Copilot CLI.

   Copilot will ask you to confirm that you trust the files in this folder.

   > \[!IMPORTANT]
   > During this GitHub Copilot CLI session, Copilot may attempt to read, modify, and execute files in and below this folder. You should only proceed if you trust the files in this location. For more information about trusted directories, see [About GitHub Copilot CLI](/en/copilot/concepts/agents/copilot-cli/about-copilot-cli#trusted-directories).

3. Choose one of the options:

   **1. Yes, proceed**:

   Copilot can work with the files in this location for this session only.

   **2. Yes, and remember this folder for future sessions**:

   You trust the files in this folder for this and future sessions. You won't be asked again when you start Copilot CLI from this folder. Only choose this option if you are sure that it will always be safe for Copilot to work with files in this location.

   **3. No, exit (Esc)**:

   End your Copilot CLI session.

4. If you are not currently logged in to GitHub, you'll be prompted to use the `/login` slash command. Enter this command and follow the on-screen instructions to authenticate.

5. Enter a prompt in the CLI.

   This can be a simple chat question, or a request for Copilot to perform a specific task, such as fixing a bug, adding a feature to an existing application, or creating a new application.

   As an alternative to typing, you can speak your prompt. See [Use voice input with Copilot CLI](/en/copilot/how-tos/copilot-cli/use-copilot-cli/voice-input).

   For some examples of prompts, see [About GitHub Copilot CLI](/en/copilot/concepts/agents/copilot-cli/about-copilot-cli).

6. When Copilot wants to use a tool that could modify or execute files—for example, `touch`, `chmod`, `node`, or `sed`—it will ask you to approve the use of the tool.

   Choose one of the options:

   **1. Yes**:

   Allow Copilot to use this tool. The next time Copilot wants to use this tool, it will ask you to approve it again.

   **2. Yes, and approve TOOL for the rest of the running session**:

   Allow Copilot to use this tool—with any options—without asking again, for the rest of the currently running session. Any pending parallel permission requests of the same type will be auto-approved. You will have to approve the command again in future sessions.

   Choosing this option is useful for many tools—such as `chmod`—as it avoids you having to approve similar commands repeatedly in the same session. However, be aware of the security implications of this option. For example, choosing this option for the command `rm` would allow Copilot to delete any file in the current directory or its subdirectories without asking for your approval.

   **3. No, and tell Copilot what to do differently (Esc)**:

   Copilot will not run the command. Instead, it ends the current operation and awaits your next prompt. You can tell Copilot to continue the task but using a different approach.

   For example, if you ask Copilot to create a bash script but you do not want to use the script Copilot suggests, you can stop the current operation and enter a new prompt, such as: `Continue the previous task but include usage instructions in the script`.

   When you reject a tool permission request, you can also give Copilot inline feedback about the rejection so it can adapt its approach without stopping entirely.

## Tips

Optimize your experience with Copilot CLI with the following tips.

### Stop a currently running operation

If you enter a prompt and then decide you want to stop Copilot from completing the task while it is still "Thinking," press <kbd>Esc</kbd>.

### Use plan mode

Plan mode lets you collaborate with Copilot on an implementation plan before any code is written. Press <kbd>Shift</kbd>+<kbd>Tab</kbd> to cycle in and out of plan mode.

### Include a specific file in your prompt

To add a specific file to your prompt, use `@` followed by the relative path to the file. For example: `Explain @config/ci/ci-required-checks.yml` or `Fix the bug in @src/app.js`. This adds the contents of the file to your prompt as context for Copilot.

When you start typing a file path, the matching paths are displayed below the prompt box. Use the arrow keys to select a path and press <kbd>Tab</kbd> to complete the path in your prompt.

### Attach images and PDFs

You can attach images and PDFs to your prompts when using a model that supports image input.

Copilot supports the following file types:

* JPEG (`.jpg`, `.jpeg`)
* PNG (`.png`)
* GIF (`.gif`)
* WEBP (`.webp`)
* PDF (`.pdf`)
* HEIC (`.heic`)
* HEIF (`.heif`)

Image and PDF attachments are available on all Copilot plans and are enabled by default, with no policy required to turn the feature on or off.

You can attach a file in the following ways during an interactive session:

* Reference the file in your prompt using `@` followed by the path to the file.
* Drag and drop a file into the interactive session.
* Copy an image to your clipboard, then paste it as an attachment.

### Work with files in a different location

To complete a task, Copilot may need to work with files that are outside the current working directory. If a prompt you have entered in an interactive session requires Copilot to modify a file outside the current location, it will ask you to approve access to the file's directory.

You can also add a trusted directory manually at any time by using the slash command:

```shell
/add-dir /path/to/directory
```

If all of the files you want to work with are in a different location, you can switch the current working directory without starting a new Copilot CLI session by using either the `/cwd` or `/cd` slash commands:

```shell
/cwd /path/to/directory
```

### Run shell commands

You can prepend your input with `!` to directly run shell commands, without making a call to the model.

```shell
!git clone https://github.com/github/copilot-cli
```

### Schedule prompts to run later

You can schedule prompts to run in the future using the `/every` and `/after` slash commands. The `/every` command schedules a prompt to run repeatedly at a specified interval, while the `/after` command schedules a one-shot prompt to run once after a specified delay. For example:

```shell
/every 1h Run frontend tests and report any failures
```

For more information, see [Scheduling prompts in GitHub Copilot CLI](/en/copilot/how-tos/copilot-cli/automate-copilot-cli/schedule-prompts).

### Resume an interactive session

You can use the `--resume` command-line option or the `/resume` slash command to select and resume an interactive CLI session, allowing you to pick up right where you left off, with the saved context. You can kick off a Copilot cloud agent session on GitHub, and then use GitHub Copilot CLI to bring that session to your local environment.

> \[!TIP]
> To quickly resume the most recently closed local session, enter this in your terminal:
>
> ```shell
> copilot --continue
> ```

### Use custom instructions

You can enhance Copilot’s performance, by adding custom instructions to the repository you are working in. Custom instructions are natural language descriptions saved in Markdown files in the repository. They are automatically included in prompts you enter while working in that repository. This helps Copilot to better understand the context of your project and how to respond to your prompts.

Copilot CLI suppor

<note>Content truncated. Call the fetch tool with a start_index of 8000 to get more content.</note>
````

</details>


---

<sub>4m 31s</sub>

### `web_fetch`

**https://docs.github.com/api/article/body?pathname=/en/copilot/concepts/agents/copilot-cli/about-copilot-cli**

<details>
<summary>Arguments</summary>

```json
{
  "url": "https://docs.github.com/api/article/body?pathname=/en/copilot/concepts/agents/copilot-cli/about-copilot-cli",
  "max_length": 6000
}
```

</details>

<details>
<summary>61 lines</summary>

````
Contents of https://docs.github.com/api/article/body?pathname=/en/copilot/concepts/agents/copilot-cli/about-copilot-cli:
# About GitHub Copilot CLI

Find out about using Copilot from the command line.

## Introduction

The command-line interface (CLI) for GitHub Copilot allows you to use Copilot directly from your terminal. You can use it to answer questions, write and debug code, and interact with GitHub.com. For example, you can ask Copilot to make some changes to a project and create a pull request.

GitHub Copilot CLI gives you quick access to a powerful AI agent, without having to leave your terminal. It can help you complete tasks more quickly by working on your behalf, and you can work iteratively with GitHub Copilot CLI to build the code you need.

## Supported operating systems

* Linux
* macOS
* Windows from within Powershell and [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/about)

For installation instructions, see [Installing GitHub Copilot CLI](/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli).

## Modes of use

GitHub Copilot CLI has two user interfaces: interactive and programmatic.

### Interactive interface

To start an interactive session, enter `copilot`. Within an interactive session, you can have a conversation with Copilot. You can prompt Copilot to perform one or more tasks, and you can give it feedback and steer the direction of the work.

![Screenshot of the Welcome message in the interactive interface of Copilot.](/assets/images/help/copilot/copilot-cli-welcome.png)

The interactive interface has two modes. In addition to the default ask/execute mode there is also a **plan mode** in which Copilot will build a structured implementation plan for a task you want to complete.

Press <kbd>Shift</kbd>+<kbd>Tab</kbd> to cycle between modes. In plan mode, Copilot analyzes your request, asks clarifying questions to understand scope and requirements, and builds a plan before writing any code. This helps you catch misunderstandings before any code is written, and stay in control of complex, multi-step tasks.

### Programmatic interface

You can also pass the CLI a single prompt directly on the command line. The CLI completes the task and then exits.

To use the CLI programmatically, include the `-p` or `--prompt` command-line option in your command. To allow Copilot to modify and execute files you should also use one of the approval options described later in this article—see [Allowing tools to be used without manual approval](#allowing-tools-to-be-used-without-manual-approval) ). For example:

```bash copy
copilot -p "Show me this week's commits and summarize them" --allow-tool='shell(git)'
```

Alternatively, you can use a script to output command-line options and pipe this to `copilot`. For example:

```bash copy
./script-outputting-options.sh | copilot
```

> \[!CAUTION]
> If you use an automatic approval option such as `--allow-all-tools`, Copilot has the same access as you do to files on your computer, and can run any shell commands that you can run, without getting your prior approval. See [Security considerations](#security-considerations), later in this article.

## Running in a sandbox with cloud and local sandboxes for GitHub Copilot

> \[!NOTE]
> Cloud and local sandboxes for GitHub Copilot is in public preview and subject to change.

Cloud and local sandboxes for GitHub Copilot provides isolated execution environments for Copilot CLI, both locally and in the cloud. For more information, see [About cloud and local sandboxes for GitHub Copilot](/en/copilot/concepts/about-cloud-and-local-sandboxes).

### Local sandboxing

You can enable local sandboxing inside a Copilot CLI session to restrict Copilot's access to your filesystem, network, and system capabilities. To enable it, run `/sandbox enable` inside a session.

### Cloud sandboxing

You can start a Copilot CLI session inside an isolated, cloud-hosted environment with cloud sandboxes. This is useful when you want to run code without affecting your local machine, keep a session's state between uses, continue a session from a different machine, or run multiple tasks in parallel. Cloud sandbox policies inherit from Copilot cloud agent policies, so existing security controls like firewall rules extend to cloud sandboxes without additional setup.

To start a cloud-backed session, run:

```bash copy
copilot --cloud
```

## Use cases for GitHub Copilot CLI

The following sections provide examples of tasks you can complete with GitHub Copilot CLI.

### Local tasks

* From within a project directory you can ask Copilot to make a change to the code in the project. For example:

  `Change the background-color of H1 headings to dark blue`

  Copilot finds the CSS file where H1 headings are defined and changes the color value.

* Ask Copilot to tell you about changes to a file:

  `Show me the last 5 changes made to the CHANGELOG.md file. Who changed the file, when, and give a brief summary of the changes they made`

* Use Copilot to help you improve the code, or documentation, in your project.

  * `Suggest improvements to content.js`

  * `Rewrite the readme in this project to make it more accessible to newcomers`

* Use Copilot to help you perform Git operations.

  * `Commit the changes to this repo`

  * `Revert the last commit, leaving the changes unstaged`

* Ask Copilot to create an application from scratch—for example, as a proof of concept.

  `Use the create-next-app kit and tailwind CSS to create a next.js app. The app should be a dashboard built with data from the GitHub API. It should track this project's build success rate, average build duration, number of failed builds, and automated test pass rate. After creating the app, give me easy to follow instructions on how to build, run, and view the app in my browser.`

* Ask Copilot to explain why a change it made is not working as expected, or tell Copilot to fix a problem with the last change it made. For example:

  `You said: "The application is now running on http://localhost:3002 and is fully functional!" but when 

<note>Content truncated. Call the fetch tool with a start_index of 6000 to get more content.</note>
````

</details>


---

<sub>4m 31s</sub>

### `web_fetch`

**https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli**

<details>
<summary>Arguments</summary>

```json
{
  "url": "https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli",
  "max_length": 5000,
  "start_index": 8000
}
```

</details>

<details>
<summary>74 lines</summary>

````
Contents of https://docs.github.com/api/article/body?pathname=/en/copilot/how-tos/use-copilot-agents/use-copilot-cli:
ts:

* Repository-wide instructions in the `.github/copilot-instructions.md` file.
* Path-specific instructions files: `.github/instructions/**/*.instructions.md`.
* Agent files such as `AGENTS.md`.

For more information, see [Adding custom instructions for GitHub Copilot CLI](/en/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions).

### Use custom agents

A custom agent is a specialized version of Copilot. Custom agents help Copilot handle unique workflows, particular coding conventions, and specialist use cases.

Copilot CLI includes a default group of custom agents for common tasks:

<table>
  <thead>
    <tr>
      <th style="width:20%">Agent</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Explore</td>
      <td>Performs quick codebase analysis, allowing you to ask questions about your code without adding to your main context.</td>
    </tr>
    <tr>
      <td>Task</td>
      <td>Executes commands such as tests and builds, providing brief summaries on success and full output on failure.</td>
    </tr>
    <tr>
      <td>General purpose</td>
      <td>Handles complex, multi-step tasks that require the full toolset and high-quality reasoning, running in a separate context to keep your main conversation clearly focused.</td>
    </tr>
    <tr>
      <td>Code review</td>
      <td>Reviews changes with a focus on surfacing only genuine issues, minimizing noise.</td>
    </tr>
    <tr>
      <td>Research</td>
      <td>Performs deep research across your codebase, relevant repositories, and the web, producing a detailed report with citations.</td>
    </tr>
    <tr>
      <td>Rubber duck</td>
      <td>Acts as a constructive critic to provide feedback on some non-trivial tasks. Used automatically by Copilot CLI.</td>
    </tr>
  </tbody>
</table>

The AI model being used by the CLI can choose to delegate a task to a subsidiary subagent process, that operates using a custom agent with specific expertise, if it judges that this would result in the work being completed more effectively. The model may equally choose to handle the work directly in the main agent.

Some built-in custom agents, such as the rubber duck agent, are consulted automatically by Copilot on your behalf rather than invoked by you directly. You won't see them as separate options when you run `/agent`, but you may see Copilot mention them as it works through a task.

You can define your own custom agents using Markdown files, called agent profiles, that specify what expertise the agent should have, what tools it can use, and any specific instructions for how it should respond.

You can define custom agents at the user, repository, or organization/enterprise level:

| Type                                           | Location                                                                                 | Scope                                                       |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| User-level custom agent                        | local `~/.copilot/agents` directory                                                      | All projects                                                |
| Repository-level custom agent                  | `.github/agents` directory in your local and remote repositories                         | Current project                                             |
| Organization and Enterprise-level custom agent | `/agents` directory in the `.github-private` repository in an organization or enterprise | All projects under your organization and enterprise account |

In the case of naming conflicts, a system-level agent overrides a repository-level agent, and the repository-level agent would override an organization-level agent.

Custom agents can be used in three ways:

* Using the slash command in the CLI's interactive interface to select from the list of available custom agents:

  ```shell
  /agent
  ```

* Calling out to custom agent directly in a prompt:

  ```shell
  Use the refactoring agent to refactor this code block
  ```

  Copilot will automatically infer the agent you want to use.

* Specifying the custom agent you want to use with the command-line option. For example:

  ```shell
  copilot --agent=refactor-agent --prompt "Refactor this code block"
  ```

For more information, see [Creating custom agents for Copilot cloud agent](/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/create-custom-agents).

### Use skills

You can create skills to enhance the ability of Copilot to perform specialized tasks with instructions, scripts, and resources.

For more information, see [Adding agent skills for GitHub Copilot CLI](/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills).

### Use hooks

You can use hooks to extend and customize the behavior of Copi

<note>Content truncated. Call the fetch tool with a start_index of 13000 to get more content.</note>
````

</details>


---

<sub>4m 54s</sub>

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

## Together: Match agent + model to your task

| Task | Agent | Model strategy |
|---|---|---|
| Deep architectural investigation | Research / General Purpose | Powerful model (Opus/GPT-5) |
| Quick "what does this file do?" | Explore | Lighter/faster model |
| Running CI, builds, tests | Task | Lighter model is fine |
| Complex refactor or new feature | General Purpose | Powerful model |
| PR review before merge | Code Review | Powerful model |
| Planning a big change | Plan mode (`Shift+Tab`) | Set dedicated model via `/model --plan` |

---

**Bottom line:** Think of `/agent` as choosing a specialist colleague, and `/model` as choosing how sharp their thinking is. For routine or mechanical tasks, a lighter model + task agent saves resources. For high-stakes reasoning, a powerful model + general-purpose or research agent gives the best results.

---

<sub>1303m 58s</sub>

### Info

Tip: /instructions

---

<sub>Generated by [GitHub Copilot CLI](https://github.com/features/copilot/cli)</sub>
