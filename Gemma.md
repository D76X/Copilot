# Gemma 

- 01 Start gemma4 local model with Ollama: `ollama run gemma4`

- 02 Start the Open-WebUI container in Docker

- 03 


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