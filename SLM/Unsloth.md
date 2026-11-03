# Unsloth

[Unsloth](https://unsloth.ai/)  
[Unsloth](https://unsloth.ai/docs/models/gemma-4) 

---

# Unsloth Studio

[Unsloth Studio Just Changed LLM Finetuning Forever AI Prompt Engineer 48](https://www.youtube.com/watch?v=pa9gBqgrJtY)  

---

# What is Unsloth for fine-tuning models?

**Unsloth** is an open-source framework designed to make fine-tuning and training large language models (LLMs) 
and vision models drastically **faster** and more **memory-efficient**.

Traditionally, fine-tuning massive models like Llama, Mistral, or Qwen required expensive enterprise 
cluster hardware with massive amounts of VRAM. Unsloth bypasses these hardware barriers, allowing developers 
and researchers to fine-tune state-of-the-art models locally on standard consumer GPUs 
(such as an NVIDIA RTX 3090, 4090, or 50-series).

---

### Key Features & Benefits

* **Extreme Speedups:** Unsloth uses custom-written kernels (utilizing Triton and hand-optimized PyTorch code) 
to speed up training significantly—often **2x to 5x faster** than standard training pipelines.

* **Massive VRAM Savings:** By optimizing memory gradients and utilizing techniques like **QLoRA** (Quantized Low-Rank Adaptation) 
and 4-bit/8-bit quantization, Unsloth reduces memory usage by up to **80%**. This lets you train larger models on smaller hardware 
without running out of memory (OOM).

* **Zero Loss in Accuracy:** Unlike some quantization methods that degrade model quality, Unsloth’s optimizations 
do not hurt the model’s final accuracy or perplexity. Math and gradient calculations remain mathematically precise.

* **Long-Context Support:** It enables efficient fine-tuning for models with extended context lengths 
(e.g., 4x longer context windows) without blowing up memory constraints.

* **Easy Export to GGUF / Ollama:** Once you finish training your model, Unsloth provides built-in tools to export 
your model into formats like **GGUF**, making it seamless to run locally using tools like **Ollama**, Llama.cpp, or vLLM.

* **Broad Model Support:** It supports a wide variety of modern architectures, including text models, vision-language models, 
and reasoning models (such as Llama, Mistral, DeepSeek, and Phi).

### Why Do People Use It?

If you want to customize an open-weights LLM with your own proprietary dataset—such as teaching it a specific writing style, 
injecting domain-specific legal or medical knowledge, or formatting it for a specific task—Unsloth makes the process practical 
on a single consumer graphics card using standard notebooks (like Google Colab or local Jupyter environments) with minimal code.

---
