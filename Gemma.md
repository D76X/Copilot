# Gemma 

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

Yes, Open WebUI uses Ollama as its primary local backend to run large language models.However, it is not strictly required.Native Integration: Open WebUI is designed to natively connect with Ollama, allowing you to manage models directly from the UI, pull new ones, and view GPU performance.No Ollama Required: You can use Open WebUI without Ollama. It also supports other OpenAI-compatible APIs (like Anthropic, OpenAI, or LocalAI). If you run it via Docker, you can disable the Ollama requirement entirely by setting the environment variable -e ENABLE_OLLAMA_API=False.

---

## Use the graphic card with Open WebUi

To use a graphics card with Open WebUI, the GPU isn't meant for the Open WebUI interface itself (which is just a frontend); instead, your GPU needs to be assigned to your backend inference engine, such as Ollama or llama.cpp.Follow these steps to set it up:1. Install the GPU Driver & ToolkitNvidia: Ensure you have your latest proprietary drivers and the NVIDIA Container Toolkit installed so Docker can access your GPU.Intel/AMD: Ensure you have ROCm (AMD) or IPEX-LLM (Intel Arc) installed.2. Run the Backend with GPU SupportYou need to pass the GPU flag to your backend (Ollama) container so it offloads Large Language Model computations to your graphics card.If you are using Docker with Nvidia, run Ollama with GPU support enabled:bashdocker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

Usa il codice con cautela.3. Run Open WebUI with GPU SupportWhile Open WebUI runs fine on a CPU, if you want to use the GPU for advanced local tasks like text-to-speech, audio transcription (Whisper), or document embeddings (for RAG), you should deploy the CUDA version of the Open WebUI container.Run the following command in your terminal:bashdocker run -d -p 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda

Usa il codice con cautela.Note: If you already have Ollama installed natively on Windows/Linux (not inside Docker), you can just run Open WebUI as normal, and it will auto-detect the Ollama instance at localhost:11434.4. Connect and VerifyOpen your browser and go to http://localhost:3000.Create your administrator account and log in.Go to Settings > Connections and ensure your Ollama API URL is set (e.g., http://localhost:11434 or http://docker.internal if Ollama is running in Docker).Go to Models in the panel to download models (e.g., llama3), which will now be processed using your graphics card.

---