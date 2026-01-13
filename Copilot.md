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

> Copilot Coding Agent
  
- Coding Agent work aysnchronously on GitHub.

---

[Use Agent Skills in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)  
[Introducing Agent Skills in VS Code Visual Studio Code](https://www.youtube.com/watch?v=JepVi1tBNEE&t=12s)  

[Level Up Your VS Code Productivity (Mastering AI Workflows) Burke Holland](https://www.youtube.com/watch?v=0XoXNG65rfg&t=37s)  
[awesome-copilot GitHub](https://github.com/github/awesome-copilot)  

The composition of a prompt that is sent upt to Copilot from the IDE:

1. The System Prompt
    - Core Identity and Global Rules
    - General Model-Specific Instruction
    - Tool-Specific Instructions (the tools in the IDE)
    - Output Format Instructions
    - **CUSTOM INSTRUCTION(S)** [appended one after the other as the appear in the ./github/instructions folder]

2. The User Prompt [1]
    - Environment Info
    - Workspace Info: the whole file structure of the project
    
3. The User Prompt [2]
    - Context Info: Current Date & Time, list of open terminal, etc.
    - Editor Context: any file that may have been added to teh chat.
    - **The User Request**

Copilot returns all teh above and the appended section **Assistant Message**. 

> CUSTOM INSTRUCTIONS

- Contain high-level information about your project to help a model to provide better answers.
- You can use the `Generate Chat Instructions` feature of GitHub Copilot to have these instructions created for you automatically by Copilot.
- Once Custom Instructions are created for a project they will be automatically included in each Chat interaction and provide GitHub Copilot and the model with more project level information.
- Any Custom Instructions will always be appended at the end of the Agent System Prompt.
- Any nummber of files with Custom Instructions can be appended to the Agent System Prompt.

> PROMPT FILES


- Prompt Files are reusable prompts that can be defined and reused in the Chat.
- It is possible to specify a model which may be used to reduce token consumption for well-known tasks.

[Use prompt files in VS Code](https://code.visualstudio.com/docs/copilot/customization/prompt-files)  

Prompt files are Markdown files that define reusable prompts for common development tasks like generating code, performing code reviews, or scaffolding project components. They are standalone prompts that you can run directly in chat, enabling the creation of a library of standardized development workflows.

They can include task-specific guidelines or reference custom instructions to ensure consistent execution. 
**Unlike custom instructions that apply to all requests, prompt files are triggered on-demand for specific tasks**.
