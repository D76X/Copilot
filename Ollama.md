# Ollama

[Ollama CLI Reference](https://docs.ollama.com/cli) 

[library of models - ollama](https://ollama.com/library)  
[gemma4 tags - ollama](https://ollama.com/library/gemma4/tags)   

All Ollama commands are of the type `ollama [cmd]`.

| Shortcut     | Effect | Description | Notes |
| :----------- | :-------: | :-----------------------------------------------------: | ----: |
| ollama       | Operation  | **EXPLAINED IN MORE DETAILS BELOW** | |
| ls           | Query      | List Models | |
| ps           | Query      | List running Models | |
| rm           | Query      | Remove a local model by name | |
| serve        | Operation  | Start Ollama | |
| run gemma4   | Operation  | Start Gemma 4 in Ollama | |
| stop gemma4  | Operation  | Stop Gemma 4 in Ollama | |
| bye          | Operation  | Exit Ollama Chat | |


---

[Ollama Tutorial: Run AI Models on Your Own Computer Teacher's Tech](https://www.youtube.com/watch?v=onrvYqir_mQ)   

---

## [Ollama FAQ](https://docs.ollama.com/faq)

---

### How can I start a local model with Ollama?

```
ollama run gemma4
ollama launch claude
ollama launch chatgpt
...
```

---

### How can I upgrade Ollama?

Ollama on macOS and Windows will automatically download updates. 
Click on the taskbar or menubar item and then click `Restart to update` to apply the update. Updates can also be installed by downloading the latest version manually.

On Linux, re-run the install script:

`curl -fsSL https://ollama.com/install.sh | sh`

---

## What is `http://localhost:11434` ?

`http://localhost:11434` is the default address and port for the Ollama API server. 
It allows developers and hobbyists to run, manage, and interact with open-source Large Language Models 
(LLMs)—such as Llama 3 or Mistral—directly on their local machine.

- Common Applications

Since Ollama acts as a backend engine, you typically connect other front-end software to this address
so you can have a ChatGPT-like interface over your private models. 

Common tools that link to this port include:

- [Open WebUI](https://openwebui.com/)  
- [LobeChat](https://app.lobehub.com/)  
- [AnythingLLM](https://anythingllm.com/)  


---

## Ollama exceeds the available context size (4096 tokens)

> Prompt

```
Can you extract the text in this image? The first three lines of text can be extracted as free text up 
to the token "session." As for the text that is located in the lower part of the image, after the token 
"session.", I would like that you extract it into a markdown table with the following columns: 
“Environment Variable“, “Required / Optional“, “Meaning“.
Try to implement this, please.
```

> Error

```
{"error":{"code":400,"message":"request (5274 tokens) exceeds the available context size (4096 tokens), try increasing it","type":"exceed_context_size_error","n_prompt_tokens":5274,"n_ctx":4096}}
```

By default, Ollama silently caps your context window to 4096 tokens even if the model you 
downloaded natively supports 32k or 128k. Once your prompt and conversation history exceed 
this limit, the model will suffer from memory loss, start hallucinating, or return an error.

Ollama caps the context window at 4096 tokens by default for most models, which causes truncation 
and memory loss during long conversations or complex tasks. You can permanently bypass this limit 
by passing a specific context parameter via 

1. your terminal
2. environment variables
3. code applications

Choose the method that best matches how you run your model:

## Method 0: In the CLI using a Modelfile (The simplest)

[Ollama 4096 token limit - Reddit](https://www.reddit.com/r/ollama/comments/1p32ism/4096_token_limit/)  

If you're using the new desktop UI, you can change the ctx size 
with the slider under the cog wheel settings menu too.

---

## Method 1: In the CLI using a Modelfile (Recommended)

This is the cleanest method because it saves the new context size permanently to your local model.

1. Create a new text file named Modelfile in your working directory.

2. Add the following lines, replacing [your-model-name] with the model you use (e.g., llama3 or qwen2.5):

```
FROM your-model-name
PARAMETER num_ctx 16384
```

3. Create the new custom model by running this command in your terminal:

`ollama create custom-model-name -f Modelfile`

4. Run your custom model: `ollama run custom-model-name`.

---

Using the Terminal (/set parameter & /save)

If you chat with models directly in the Ollama terminal, you can easily increase the window for 
your current session and save it as a new model:

---