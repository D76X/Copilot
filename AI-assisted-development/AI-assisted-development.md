# Advanced AI-assisted Development

[AI-Assisted Coding Path](https://app.pluralsight.com/learning-paths/4ccabe1e-91ee-45eb-95a0-6224e0f35bdd)  

[Advanced AI-assisted Development - Michael Perry](https://app.pluralsight.com/ilx/video-courses/advanced-ai-assisted-development/course-overview)

1. Managing Context
2. Build Agents
3. Orchestrationg Workflows and processes
4. Automating the software development lifecycle

# Summary

- The role of the development team shifts from writing code to maintaining software factories
- Transition from using AI as a software contributor to leading a AI-assisted development team
- Focus on techniques and NOT tools, because the tools evolve too rapidly

---

## Managing Context

# Context Management

[Context Management Strategy](https://app.pluralsight.com/ilx/video-courses/abc09662-ba46-4266-9dd1-40ebc4d4d67b/2d9bf3ce-1c64-4138-a466-6b8672c5b1a0/7c515fdf-24a9-4f09-a783-825938fdb5e7)  

- context is valuable and limited; it must be managed well
- keep the comntext narrow and controlled

| Goal | Technique |
| ----------------------------- | ---------------------------- |
| Ensure complete information   | Fill the bucket              |
| Prevent incorrect information | Avoid context poisoning      |
| Use specific information      | Inject focused documentation |
| Constrain to team decisions   | Record project culture       |

---

# [Inject focused documentation](https://app.pluralsight.com/ilx/video-courses/abc09662-ba46-4266-9dd1-40ebc4d4d67b/2d9bf3ce-1c64-4138-a466-6b8672c5b1a0/fd546f9a-b7ef-46ad-ae6c-de6fe26daa45)  

---

# [Avoid Context Poisoning](https://app.pluralsight.com/ilx/video-courses/abc09662-ba46-4266-9dd1-40ebc4d4d67b/2d9bf3ce-1c64-4138-a466-6b8672c5b1a0/6e5f0d6e-84ce-41fc-9750-d44cbf3f6108)  

Prevent incorect information from enetring the cotext.

In the context:

- give specifics details 
- give specifics guidance
- start a new session with erroneous information removed or with a clean summary from the old session
- the best option is always to start from scratch

---

# [Fill the bucket](https://app.pluralsight.com/ilx/video-courses/abc09662-ba46-4266-9dd1-40ebc4d4d67b/2d9bf3ce-1c64-4138-a466-6b8672c5b1a0/73951fd7-c8f0-4510-ac3a-10b679a8ea04)  

## Iterate between AK mode and PLAN mode

- select ask mode
- use the LLM to fill the bucket, i..e. exploring a prarticular problem with the code base / architecture
- ask the model to provide implementation options to solve a particular problem
- after reviewing the options select one and ask the agent to produce a step-by-step summary implementation plan
- start a NEW session to clear the context
- swicth to plan mode
- crete an implementatin plan fom the step-by-step summary implementation plan
- switch backl to ask mode to REVIEW the implementation plan
- REVIEW the steps of the implementation plan
- ask specific questions

##

---
