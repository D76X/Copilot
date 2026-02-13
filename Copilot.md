# Copilot

# Copilot in VS Code

[GitHub Copilot Fundamentals: AI Agents by Aaron Steward](https://app.pluralsight.com/ilx/video-courses/63ef6a3d-992d-4586-8c0c-760479bbad95/c1105e40-64c1-41c6-9dba-fd28f80a23d9/f49a1885-4902-41a8-8336-210eb6235171)   

> Copilot Chat

- The intuitive interactive natural conversational interface.
- This chat may be installed and shipped with a variaty of IDEs.

> Copilot Edits: a feature of Copilot Chat

- It allows to iterate on code changes accross multiple files within the editor using natural language promps.
- It provides a side-by-side comparison of proposed changes.
- The user can review, accept or reject the changes individually or collectively.
- The objective is to streamline code changes.

> Copilot Code Reviews

- It delegates the code review to a Copilot Agent
- Identify performance issues
- Identify bugs
- Recommend bug fixes
- The objective is to streamline code reviews reducing their time demand.

> Agent Mode

- A real-time collaborator that is present in the editor.
- Agent Mode work aysnchronously in the IDE. 

[The Ultimate Agent Mode Tutorial in VS Code: Vision, MCP, Custom Agents & More! Visual Studio Code](https://www.youtube.com/watch?v=5NxGqnTazR8)  

> Copilot Coding Agent
  
- Coding Agent work aysnchronously on GitHub.

---

# Copilot Chat in VS Code - Anatomy

[Level Up Your VS Code Productivity (Mastering AI Workflows) Burke Holland](https://www.youtube.com/watch?v=0XoXNG65rfg&t=37s)  
[Introducing the Awesome GitHub Copilot Customizations repo](https://developer.microsoft.com/blog/introducing-awesome-github-copilot-customizations-repo)  

[awesome-copilot GitHub](https://github.com/github/awesome-copilot)  
[awesome-copilot GitHub - Structured Autonomy - Burke Holland](https://github.com/github/awesome-copilot/blob/main/collections/structured-autonomy.md)   


The composition of a prompt that is sent upt to Copilot from the IDE:

1. The System Prompt
    - Core Identity and Global Rules
    - General Model-Specific Instruction
    - Tool-Specific Instructions (the tools in the IDE)
    - Output Format Instructions
    - **CUSTOM INSTRUCTION(S)** [appended one after the other as the appear in the ./github/instructions folder]
    - **CUSTOM AGENT**

2. The User Prompt [1]
    - Environment Info
    - Workspace Info: the whole file structure of the project
    
3. The User Prompt [2]
    - **PROMPT FILES** ( these can refer to **CUSTOM INSTRUCTION(S)**)
    - Context Info: Current Date & Time, list of open terminal, etc.
    - Editor Context: any file that may have been added to teh chat.
    - **The User Request** (this can refer to **PROMPT FILES**)

Copilot returns all the above and the appended section **Assistant Message**. 

> AGENTIC WORKFLOW

The main objective of **CUSTOM INSTRUCTION(S), PROMPT FILES and CUSTOM AGENT** is to compose (define) an **AGENTIC WORKFLOW**.

---

> CUSTOM INSTRUCTIONS AND INSTRUCTION FILES

[Use custom instructions in VS Code](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)  
[awesome-copilot>instructions](https://github.com/github/awesome-copilot/tree/main/instructions)  
[Code It With AI - Mastering Copilot Prompts & Instructions in .NET (ep.2) DevExpress](https://www.youtube.com/watch?v=TCPeccH5M3g&t=644s)  
[Prompt Files and Instructions Files Explained Wendy Breiding (SHE/HER) .Net Blog](https://devblogs.microsoft.com/dotnet/prompt-files-and-instructions-files-explained/)  

Custom instructions enable you to define common guidelines and rules that automatically 
influence how AI generates code and handles other development tasks. Instead of manually 
including context in every chat prompt, specify custom instructions in a Markdown file 
to ensure consistent AI responses that align with your coding practices and project 
requirements.

- Contain high-level information about your project to help a model to provide better answers.
- You can use the `Generate Chat Instructions` feature of GitHub Copilot to have these instructions created for you automatically by Copilot.
- Once Custom Instructions are created for a project **they will be automatically included in each Chat interaction** and provide GitHub Copilot and the model with more project level information.
- Any Custom Instructions will always be appended at the end of the Agent System Prompt.
- Any nummber of files with Custom Instructions can be appended to the Agent System Prompt.

- It is important to remeber that instructions are included **they will be automatically included in each Chat interaction** and can cause the overall **User Prompt** to grow considerably. You can use the `applyTo` field of the instruction file to set a **file filter** that limits its scope.

> How do I avoid the instruction files from growing large in the User Prompt in Copilot?

To avoid having instruction files grow too large and consume the context window in Copilot (particularly in GitHub Copilot Chat), 
you should adopt a modular approach. 
**Keep instructions concise, targeted, and separated by topic rather than using a single, comprehensive file**. 

1. Structure Instructions Modularly

- Split into Smaller Files: 
Instead of one massive 700-line instruction file, create multiple smaller, specialized files in the `.github/instructions/` folder.

- Use Specific Context: 
Place instructions that only apply to certain file types (e.g., .cs or .razor) in dedicated, smaller instruction files within the `.github/instructions/` directory.

- Use AGENTS.md: 
For specialized roles, use `AGENTS.md` files to keep prompt context focused. 

2. Optimize and Compress Content

- Be Concise and Direct: 
Ensure instructions are clear and to the point. 
Avoid long, verbose explanations. 
Define the goal, but keep it concise.

- Summarize Documentation: 
Before uploading files for reference, summarize them. 
If a file is too large, it may cause errors or be ignored by the LLM.

- Compress Files: 
Use PDF compression or ZIP files for larger reference documents to keep them under the `10MB–512MB` limit. 

3. Use Strategic Prompt Engineering 

- Prioritize Important Information: 
Place key instructions at the beginning or end of your file, as Large Language Models tend to prioritize this information.

- Remove Unnecessary Details: 
Only include information that is absolutely necessary for the task at hand.

- Use Variables (Copilot Studio): 
If using `Copilot Studio`, define specific variables for the payload rather than passing entire, large datasets. 

4. Technical Workarounds

- Use External Storage: 
Instead of uploading large files, store them in SharePoint (up to 200MB+ depending on licenses) 
or Azure Blob Storage and provide the reference to Copilot.

- Use Notebook for Long Text: 

[Get started with Microsoft 365 Copilot Notebooks](https://support.microsoft.com/en-us/topic/get-started-with-microsoft-365-copilot-notebooks-0775e693-11c6-4d80-8aba-fcc81a737a06)   

If you are copying and pasting long text, use the `Notebook feature` in Copilot to better manage long-context input.
Copilot Notebook is an AI-powered, intelligent workspace in Microsoft 365 designed for deep, grounded analysis of large documents (Word, PowerPoint, PDFs, Loop) and project-specific chat, rather than quick, ephemeral queries. 
It allows users to centralize content in OneNote or the web app, offering features like customized prompting, real-time file updates, and summarization, requiring a Microsoft 365 Copilot license. 

- Break Up Long Tasks: 
Split large documents by chapter, section, or page, and feed them to Copilot in chunks, 
asking for summaries or analysis on each part separately. 

5. Guidelines on File Size

- Optimal Document Length: 
Aim for under `20 pages` or around `15,000 words` for optimal performance in `M365 Copilot`.

- Character Limits: 
Note that instructions in Copilot Studio are often limited to `8,000 characters per agent`. 

> Examples

One example use case for CUSTOM INSTRUCTIONS AND INSTRUCTION FILES is when you want to 
have specific instructions for each technology stack you work with. 


> PROMPT FILES

[awesome-copilot>prompts](https://github.com/github/awesome-copilot/tree/main/prompts)  

- Prompt Files are reusable prompts that can be defined and reused in the Chat.
- It is possible to specify a model which may be used to reduce token consumption for well-known tasks.

[Use prompt files in VS Code](https://code.visualstudio.com/docs/copilot/customization/prompt-files)  

Prompt files are Markdown files that define reusable prompts for common development tasks like generating code, 
performing code reviews, or scaffolding project components. They are standalone prompts that you can run directly
in chat, enabling the creation of a library of standardized development workflows.

They can include task-specific guidelines or **reference custom instructions** to ensure consistent execution. 
**Unlike custom instructions that apply to all requests, prompt files are triggered on-demand for specific tasks**.

> CUSTOM AGENTS

- They used to be called **CUSTOM MODES**.
- The basic idea is to buid instructions to override an agent's default behaviour.
- The **CUSTOM AGENTS** is special because it is **always appended to the System Prompt**.

[Custom agents in VS Code](https://code.visualstudio.com/docs/copilot/customization/custom-agents)  
[awesome-copilot>agents](https://github.com/github/awesome-copilot/tree/main/agents)  

The built-in agents provide general-purpose configurations for chat in VS Code. 
For a more tailored chat experience, you can create your own custom agents.
Custom agents consist of a set of instructions and tools that are applied when you switch to that agent.
For example, a "Plan" agent could include instructions for generating an implementation plan and only use read-only tools.
Custom agents are defined in a `.agent.md` Markdown file.

Custom agents enable you to configure the AI to adopt different personas tailored to specific development roles and tasks. 
For example, you might create agents for a security reviewer, planner, solution architect, or other specialized roles. 
Each persona can have its own behavior, available tools, and instructions.

**The focus of any custom agent is to define a specific identity for the operation of the agent**, 
this is very different from what is done with **CUSTOM INSTRUCTIONS** with which a sequence of instructions 
that is provided to a plain built-in agent.

> AGENT SKILLS

[Use Agent Skills in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)  
[Introducing Agent Skills in VS Code Visual Studio Code](https://www.youtube.com/watch?v=JepVi1tBNEE&t=12s)  
[The complete guide to Agent Skills Burke Holland](https://www.youtube.com/watch?v=fabAI1OKKww)  

[awesome-copilot>skills](https://github.com/github/awesome-copilot/tree/main/skills)  

> CHAT PARTICIPANTS

[Chat Participant API](https://code.visualstudio.com/api/extension-guides/ai/chat)   
[Building your own GitHub Copilot chat participant in VS Code Visual Studio Code](https://www.youtube.com/watch?v=OdW2r3raAHI)   

[GitHub Copilot's @Workspace - Deep Dive Visual Studio Code](https://www.youtube.com/watch?v=3Yz48eenPEE)   
[The technology behind GitHub’s new code search](https://github.blog/engineering/the-technology-behind-githubs-new-code-search/)   
[Language Server Extension Guide](https://code.visualstudio.com/api/language-extensions/language-server-extension-guide)  
[How to Search And Find Anything In VSCode hUndefined](https://www.youtube.com/watch?v=PB5uSRFfZQ0)  
[VS Code Language Intelligence - IntelliSense](https://code.visualstudio.com/docs/editing/intellisense#:~:text=VS%20Code%20IntelliSense%20features%20are,pop%20up%20as%20you%20type.)  

[Shash Commands in Depth - GitHub Copilot Certification](https://notes.kodekloud.com/docs/GitHub-Copilot-Certification/Advanced-Features/Slash-Commands-in-Depth)
[GitHub Copilot in VS Code cheat sheet - Slash commands](https://code.visualstudio.com/docs/copilot/reference/copilot-vscode-features#_slash-commands)  

Chat participants are specialized assistants that enable users to **extend chat in VS Code with domain-specific experts**. 
Users invoke a chat participant by `@-mentioning` it, and the participant is then responsible for handling the user's 
natural language prompt.

VS Code has several built-in chat participants like 

- `@vscode`
- `@terminal` 
- `@workspace` 

They are optimized to answer questions about their respective domains.

Chat participants **are different from language model tools**. 

> LANGUAGE MODEL TOOLS

[Language Model Tool API](https://code.visualstudio.com/api/extension-guides/ai/tools)  

Language model tools enable you to **extend the functionality of a large language model (LLM) in chat with domain-specific capabilities**. 
To process a user's chat prompt, agents in VS Code can automatically invoke these tools to perform specialized tasks as part of the conversation.

---

# AGENT MODE

[VS Code Agent Mode Just Changed Everything Visual Studio Code](https://www.youtube.com/watch?v=dutyOc_cAEU)   

---

# MCP Servers [Model Context Protocol (MCP)]


[Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)   

[The Future of AI in VS Code: MCP Servers Explained! Burke Holland](https://www.youtube.com/watch?v=Wp0p7iKH6ho)  

[10 Microsoft MCP Servers to Accelerate Your Development Workflow](https://developer.microsoft.com/blog/10-microsoft-mcp-servers-to-accelerate-your-development-workflow)   

[What is MCP? - Microsoft](https://developer.microsoft.com/blog/microsoft-partners-with-anthropic-to-create-official-c-sdk-for-model-context-protocol)     

[What is the Model Context Protocol (MCP)?](https://modelcontextprotocol.io/docs/getting-started/intro)  

[Model Context Protocol servers](https://github.com/modelcontextprotocol/servers/blob/main/README.md)  

This repository is a collection of reference implementations for the Model Context Protocol (MCP), 
as well as references to community-built servers and additional resources.

The Model Context Protocol (MCP) is an open protocol created by Anthropic to enable integration 
between LLM applications and external tools and data sources. 
It was originally released in November 2024 and recently was updated to add new streaming capabilities. 
The protocol is designed to be extensible and flexible, allowing developers to create custom tools and 
data sources that can be used with LLMs.

A number of Microsoft products have already added support for MCP including: 

- [Copilot Studio](https://www.microsoft.com/en-us/microsoft-copilot/blog/copilot-studio/introducing-model-context-protocol-mcp-in-copilot-studio-simplified-integration-with-ai-apps-and-age
nts/)  
- [VS Code’s new GitHub Copilot agent mode](https://code.visualstudio.com/blogs/2025/02/24/introducing-copilot-agent-mode)  
- [Semantic Kernel](https://devblogs.microsoft.com/semantic-kernel/integrating-model-context-protocol-tools-with-semantic-kernel-a-step-by-step-guide/)  

And many Microsoft products are creating MCP servers to access their functionality. 


Some popular examples, with many more in the works:

- GitHub MCP Server 

- Playwright MCP for browser automation are 


> Videos about MCP Servers:

[VS Code Agent Mode Just Changed Everything Visual Studio Code](https://www.youtube.com/watch?v=dutyOc_cAEU)   > Introduces the concept of MCP Server  
[01-Code It With AI - Generating Documentation (ep.1)](https://www.youtube.com/watch?v=RewtTswNdHY&list=PL8h4jt35t1whFkEryOz94bu2KQPY48HLy&index=14)   
[MCP Servers in VS Code Visual Studio Code](https://www.youtube.com/watch?v=Coot4TFTkN4)   
[MCP Servers in VS Code and GitHub Copilot Visual Studio Code](https://www.youtube.com/watch?v=vUQfqW5GKAQ)  


### MCP Servers Examples

[MCP Registry for Visual Studio Code](https://github.com/mcp?utm_source=vscode-website&utm_campaign=mcp-registry-server-launch-2026)  
[Official MCP Registry Discover Model Context Protocol servers](https://registry.modelcontextprotocol.io/)  
[Model Context Protocol servers GitHub Reference Implementations](https://github.com/modelcontextprotocol/servers)  
[Awesome MCP Servers](https://mcpservers.org/)  
[MCP SO - Find Awesome MCP Servers and clients](https://mcp.so)    

> Some handy MCP Servers:

[Perplexity MCP Server](https://docs.perplexity.ai/guides/mcp-server)   

[PostgreSQL MCP Server](https://www.cdata.com/drivers/postgresql/mcp/?kw=postgresql%20mcp%20server&cpn=23029248957&_bt=775957453612&_bk=postgresql%20mcp%20server&_bm=e&_bn=g&_bg=187103520153&utm_source=google&utm_medium=cpc&utm_campaign=Search_-_Connect_AI_-_Source_-_PostgreSQL&utm_content=PostgreSQL_-_General_MCP&utm_term=e|postgresql%20mcp%20server&kw=postgresql%20mcp%20server&cpn=23029248957&gad_source=1&gad_campaignid=23029248957&gbraid=0AAAAADmmIIjqUcLWz1tQGyd1x2uOjCJGg&gclid=CjwKCAiA1obMBhAbEiwAsUBbIrjMsC9rS30xP5veqM9m7-goV2KeOWeWRk2Y1ZDiKXYzsciQZwHJzhoCQhIQAvD_BwE) 



---

# [Code It With AI - Playlist by DevExpress](https://www.youtube.com/playlist?list=PL8h4jt35t1whFkEryOz94bu2KQPY48HLy)  

[Code-it-with-AI GitHub](https://github.com/Code-it-with-AI)  
[copilotthatjawn](https://copilotthatjawn.com/)  

---

## 01 Generate Documentation

[01-Code It With AI - Generating Documentation (ep.1)](https://www.youtube.com/watch?v=RewtTswNdHY&list=PL8h4jt35t1whFkEryOz94bu2KQPY48HLy&index=14)  
[01-Code-it-with-AI GitHub Episode 01](https://github.com/Code-it-with-AI/Episode-01)  

---

## 02 Use Custom Instraction Files & Prompt Files to specialize workflow and enforce coding standards and provide Agent personality

[Code It With AI - Mastering Copilot Prompts & Instructions in .NET (ep.2) DevExpress](https://www.youtube.com/watch?v=TCPeccH5M3g&t=644s) 

---

## 03 Integrate AI Workflow with GitHub Actions 

[Code It With AI - Build & Test .NET Apps with GitHub Copilot (Ep. 3) DevExpress](https://www.youtube.com/watch?v=1eCrAsrOdoE&list=PL8h4jt35t1whFkEryOz94bu2KQPY48HLy&index=14)  

---

## Enable Models In GitHub

[Code It With AI - Build Your First .NET AI App (Using GitHub + GPT-5 Mini) (Ep. 4) DevExpress](https://www.youtube.com/watch?v=9F7muWd4sow)  

---

## Turn a paragraph of text into a schedule

[Code It With AI - .NET + AI: Parse Natural Language into Calendar Events (ep.5) DevExpress](https://www.youtube.com/watch?v=WcR6bRnoaxA&t=15s)  

---


[10-Code It With AI - Building Custom Agents (ep.10)](https://www.youtube.com/watch?v=3xoxuSNX2zw)  

[14-Code It With AI - AvnDataGenie Part 2 (ep.14) DevExpress](https://www.youtube.com/watch?v=HxyN6zUkMaE)  

---

# Perplexity in VS Code

[Perplexity MCP Server](https://docs.perplexity.ai/guides/mcp-server)   

[How to Use Perplexity AI in VS Code (Step-by-Step Tutorial) 2026 Checkmark Academy](https://www.youtube.com/watch?v=N7SiKGT8cig)  

[How to Use Perplexity in VSCode - Step By Step Mindly Nova](https://www.youtube.com/watch?v=92SrraBgr3c)   

[How To USE Perplexity In VSCode (QUICK GUIDE) 2026 InstantHowTo](https://www.youtube.com/watch?v=8armBUpmlo4)  

[AI Agents that can use Perplexity for AI search [Perplexity MCP] Voiceflow](https://www.youtube.com/watch?v=EhnfS4V5-j8)  

---

