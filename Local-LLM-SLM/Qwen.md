# Qwen

---

# Video

[Qwen 3.8 Locally: How Much Can You Actually Trust It? Zero to MVP](https://www.youtube.com/watch?v=dTutfoSVMq4)   

[Is Qwen 3.8 27b The New King of the Local LLMs? Gary Explains](https://www.youtube.com/watch?v=An4_SCFo5-A&t=61s) 

[Qwen3.8 27B is something else.. Caleb Writes Code](https://www.youtube.com/watch?v=3WbXyUolFA0)  

[Qwen3.6 Code it with AI - Language Model Roundup 2 (ep.30) DevExpress](https://www.youtube.com/watch?v=IAnaqod_lwE&list=PL8h4jt35t1whFkEryOz94bu2KQPY48HLy&index=20)

---

# Which of the Qwen models could I run on a Windows 11 PC with 64 GB of RAM shared with the graphic card?

---

# Answer from Perplexity

With 64 GB of RAM shared between system and GPU on Windows 11, you can comfortably run **Qwen models up to about 27–35B parameters** at 4‑bit quantization (GGUF Q4_K_M), and even some larger mixture‑of‑experts variants if you accept tighter memory headroom. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)

## Quick recommendation

For your hardware, the sweet spot is:

- **Qwen3.8‑27B (Q4_K_M GGUF)** – best overall quality/size balance; needs ~24 GB RAM, leaving plenty of headroom for context and other apps. [promptquorum](https://www.promptquorum.com/local-llms/best-local-llms-2026)

- **Qwen3.5‑35B‑A3B (Q4_K_M)** – a strong MoE alternative; fits in ~20 GB VRAM/RAM at Q4, so also fine on 64 GB total. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)

Anything much above that (e.g., 70B+ dense models) will start to consume 40–50+ GB just for weights, leaving little room for long contexts or multitasking. [needtoknowit.com](https://needtoknowit.com.au/blog/what-llms-actually-run-on-16gb-32gb-and-64gb-ram/)

## Model options that fit well on 64 GB

### Excellent fit (plenty of headroom)

- **Qwen3.8‑27B**  
  - ~24 GB RAM at Q4_K_M. [promptquorum](https://www.promptquorum.com/local-llms/best-local-llms-2026)
  - Strong generalist: coding, reasoning, long context (up to 262K, optionally 1M). [promptquorum](https://www.promptquorum.com/local-llms/best-local-llms-2026)
  - Ideal if you want one high‑quality model for daily use.

- **Qwen3.6‑27B / Qwen3‑32B**  
  - ~17–20 GB (27B) and ~19 GB (32B) at Q4_K_M. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)
  - Slightly lighter than 3.8‑27B; great if you also run other workloads.

### Good fit (still comfortable)

- **Qwen3.5‑35B‑A3B (MoE)**  
  - ~19.6 GB at Q4_K_M. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)
  - Mixture‑of‑experts architecture: high capability with moderate memory use.

- **Qwen2.5‑72B at Q4_K_M**  
  - Around 47 GB for weights before runtime overhead. [needtoknowit.com](https://needtoknowit.com.au/blog/what-llms-actually-run-on-16gb-32gb-and-64gb-ram/)
  - Technically possible on 64 GB, but you’ll have limited context length and little room for other apps; only if you really need 70B‑class quality.

### Smaller, very fast options

If you want very fast, low‑latency inference or plan to run multiple models:

- **Qwen3.5‑9B** – ~5.7 GB at Q4. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)
- **Qwen3‑14B** – ~8.3 GB at Q4_K_M. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)
These leave lots of RAM for very long contexts, RAG pipelines, or running other tools.

## Practical setup on Windows 11

You don’t need a dedicated high‑VRAM GPU; with 64 GB shared memory you can run these models via:

- **Ollama** (simplest):  
  - Example: `ollama pull qwen3.8:27b` then `ollama run qwen3.8:27b`. [promptquorum](https://www.promptquorum.com/local-llms/best-local-llms-2026)
- **LM Studio** or **KoboldCPP / llama.cpp**:  
  - Download a **GGUF Q4_K_M** file for your chosen Qwen variant and load it; the tool will use CPU + shared GPU memory automatically. [promptquorum](https://www.promptquorum.com/local-llms/run-qwen-locally-guide-2026)

Rule of thumb for RAM usage (very rough):  
\[
\text{RAM (GB)} \approx \frac{\text{params (B)} \times \text{bits per weight}}{8} \times 1.1
\]  
So a 27B model at 4 bits: \(27 \times 4 / 8 \times 1.1 \approx 14.85\) GB for weights, plus KV cache and overhead → ~20–24 GB in practice, matching observed numbers. [promptquorum](https://www.promptquorum.com/local-llms/best-local-llms-2026)

## Suggested choice for you

Given your background and likely use cases (coding, architecture docs, experimentation):

- **Primary model:** **Qwen3.8‑27B (Q4_K_M)** via Ollama or LM Studio. [promptquorum](https://www.promptquorum.com/local-llms/best-local-llms-2026)
- **Secondary, lighter model:** **Qwen3.5‑9B** or **Qwen3‑14B** for fast, local “copilot” style tasks. [willitrunai](https://willitrunai.com/blog/qwen-3-gpu-requirements)

If you tell me your typical context length (e.g., “I often paste 20–50k tokens of code/docs”) and whether you care more about coding vs. general reasoning, I can narrow this to a single best model and quantization level for your exact workflow.

---

# Answer from Google Gemini

With 64 GB of system RAM shared with an integrated graphics card on a Windows 11 PC (such as an AMD Ryzen AI APU or Intel Core Ultra), 
your computer functions similarly to a unified memory system. While Windows dynamically allocates about half of your system memory (~32 GB) 
as "Shared GPU Memory" by default, modern local AI runners can tap into your full RAM pool using CPU/GPU offloading.

You can comfortably and efficiently run any Qwen model up to the 32B/35B size tier, 
while 72B models will fit but run painfully slow.

------------------------------

## 🟢 The "Sweet Spot" (Fast & Highly Capable)

These models fit entirely into your RAM with plenty of headroom for Windows 11, 
background apps, and a large context window. 

They will run with excellent responsiveness.

* Qwen2.5-14B / Qwen3-14B (Quantized Q4_K_M or Q8_0):

* Memory footprint: ~9 GB (Q4) to ~15 GB (Q8).
   * Experience: Blazing fast. You can maximize the context window up to 32k+ tokens without performance degradation.

* Qwen2.5-32B / Qwen3.8-27B / Qwen3.6-35B-A3B (Quantized Q4_K_M):

* Memory footprint: ~19 GB to ~24 GB.
   * Experience: This is your best intelligence-to-speed tier. A 4-bit quantization leaves roughly 40 GB of RAM free for your operating system and a healthy text memory cache. This delivers top-tier coding, math, and reasoning locally.

## 🟡 The "Hard Limit" (Fits, but sluggish)

* Qwen2.5-72B / Qwen3-72B (Highly Quantized IQ2_M or Q3_K_L):
* Memory footprint: ~30 GB to ~42 GB.
   * Experience: Not recommended for daily use. While a heavily compressed 2-bit or 3-bit version technically fits inside your 64 GB pool, running a 72B model across system RAM shared with an integrated GPU hits a severe memory bandwidth bottleneck. Expect sluggish speeds of just 1 to 3 tokens per second.

------------------------------
## 🛠️ Optimization Tips for Shared RAM

   1. Increase Dedicated VRAM (BIOS): Restart your PC, enter the BIOS, and look for "UMA Frame Buffer Size" or "Integrated Graphics Allocation". \
   If it is set to a low default (like 512MB or 2GB), increase it to 8GB or 16GB. This forces Windows to reserve a larger slice specifically for 
   the graphics processor, which accelerates prompt processing.
   
   2. Stick to GGUF Formats: Run GGUF format models using tools like LM Studio or Ollama. They are specifically built to split the workload 
   cleanly between your CPU cores and integrated graphics.
   
   3. Target 4-bit Quantization: Always look for model files appended with Q4_K_M or IQ4_NL. They retain over 99% of the full-sized model's 
   intelligence while cutting the memory footprint in half.

To help narrow down the perfect setup, let me know:

* What is your primary use case (e.g., coding, creative writing, or general chat)?
* Do you have a preferred local software (like Ollama, LM Studio, or AnythingLLM) already installed?

---

# What are the available Qwen models by size?

Qwen models span a broad spectrum of sizes, ranging from 
ultra-small 0.5B-0.8B variants for mobile devices 
up to massive 2.4-trillion-parameter Mixture-of-Experts (MoE) flagships. [1, 2, 3] 

## Available Model Sizes

* Tiny / Edge Sizes (0.5B to 0.8B): Designed to run directly on smartphones and resource-constrained edge devices. [2, 3] 

* Small Sizes (1.5B to 4B): Fast, lightweight local dense models suitable for basic tasks and lower VRAM setups. [3, 4] 

* Mid Sizes (7B to 9B / 27B to 32B): The workhorse parameter tier across the family (including base, coder, math, and vision versions) offering high performance on consumer hardware. [3, 4, 5, 6] 

* Large / Flagship Dense & MoE Sizes (72B to 480B+): High-capacity open weights and cloud-tier APIs (such as MoE variants with active parameter subsets like Qwen3-235B-A22B or large coder/max options scaling into hundreds of billions and trillion-parameter architectures like Qwen3.8-Max at 2.4T). [1, 2, 7] 

[1] [https://www.mindstudio.ai](https://www.mindstudio.ai/blog/qwen-3-8-max-benchmarks-features)
[2] [https://www.secondtalent.com](https://www.secondtalent.com/resources/every-qwen-ai-model-explained-compared/)
[3] [https://www.youtube.com](https://www.youtube.com/watch?v=8jZSxZfdnm4)
[4] [https://canirun.ai](https://canirun.ai/company/alibaba/)
[5] [https://www.reddit.com](https://www.reddit.com/r/LocalLLaMA/comments/1i4w47k/a_summary_of_qwen_models/)
[6] [https://www.youtube.com](https://www.youtube.com/watch?v=OE5KdF4spss)
[7] [https://kilo.ai](https://kilo.ai/models/by/qwen)

---

# Is Qwen very good for coding and software architecture?

Yes, Qwen is considered one of the strongest model families for coding, 
particularly among open-weight models. Its effectiveness for software 
architecture depends heavily on the model size you choose. 

[1] (https://www.secondtalent.com/resources/qwen-ai-for-coding-reviews-usage-and-performance/), 
[2] (https://www.reddit.com/r/LocalLLaMA/comments/1uqzjdy/qwen3627b_does_not_understand_software/), 
[3] (https://macaron.im/blog/is-qwen-3-5-good-for-coding)

`Alibaba's Qwen lineup` includes flagship general-purpose models (such as `Qwen 3.8-Max` and the `Qwen 4-Max` preview) alongside specialized coding models (`Qwen3-Coder`). 

[1] (https://qwen.ai/blog?id=qwen3.8), 
[2] (https://www.yottalabs.ai/post/qwen-4-release-date-what-is-known-how-to-prepare-2026), 
[3] (https://github.com/QwenLM/Qwen3-Coder)

## Strengths in Coding

- Top-tier benchmarks. Flagship releases like `Qwen 3.8-Max` and specialized models like 
`Qwen3-Coder-Next` score competitively on real-world software engineering benchmarks like 
`SWE-bench Pro` and `Terminal-Bench`. 

[1] (https://qwen.ai/blog?id=qwen3-coder-next), 
[2] (https://qwen.ai/blog?id=qwen3.8)

- Agentic workflows. 
Newer Qwen models are trained for multi-step execution, repository-level edits, and terminal usage. 
`They integrate with coding agents like Claude Code, Cline, and Qwen Code`. 

[1] (https://qwen.ai/blog?id=qwen3.6-27b), 
[2] (https://github.com/QwenLM/Qwen3-Coder), 
[3] (https://qwen.ai/blog?id=qwen3-coder-next)

- Large context windows. 
Most modern Qwen models support `262K tokens` natively and can stretch up to `1 million tokens`. 
This lets you feed entire repositories or large documentation sets into a single prompt. 

[1] (https://qwen.ai/blog?id=qwen3.8-flash-next), 
[2] (https://vipjavascript.com/blog/qwen-3-5-comprehensive-guide)

- Local efficiency. 
`Mixture-of-Experts (MoE) variants` like `Qwen3-Coder-Next (80B total parameters, 3B active)` and 
`Qwen3.8-Flash-Next (125B total, 6B active)` deliver fast inference on consumer hardware while 
maintaining high code quality. 

[1] (https://dev.to/sienna/qwen3-coder-next-the-complete-2026-guide-to-running-powerful-ai-coding-agents-locally-1k95), 
[2] (https://qwen.ai/blog?id=qwen3.8-flash-next)

## Performance in Software Architecture

- Flagship models excel at system design. Massive reasoning models like `Qwen 3.8-Max (2.4T parameters)` 
handle complex, long-horizon planning, cross-file refactoring, and high-level architectural trade-offs well.

- Smaller models struggle with big-picture design. While smaller dense models (such as the `27B variants`) write clean functions and fix bugs quickly, they can lose architectural coherence across large codebases.

- `Quantization impacts architectural reasoning`. One point of agreement among users on `r/LocalLLaMA` 
is that heavy compression (such as 4-bit quantization) degrades a model's grasp of software architecture, 
even if basic coding benchmarks look fine. Running models at `5-bit, 8-bit`, or unquantized weights 
preserves design reasoning. 

[1] (https://www.reddit.com/r/LocalLLaMA/comments/1uqzjdy/qwen3627b_does_not_understand_software/), 
[2] (https://qwen.ai/blog?id=qwen3.8), 
[3] (https://qwen.ai/blog?id=qwen3.6-27b)

## Choosing the Right Qwen Model

- Use Case	Recommended Model	Key Specs

System Architecture & Complex Planning	Qwen 3.8-Max or Qwen 4-Max (Preview)	Flagship reasoning models designed for long-horizon tasks and multi-file system design.

Agentic Coding & Local Workstations	Qwen3-Coder-Next	80B MoE (3B active parameters); optimized for local coding agents and fast tool use.

Mid-Range GPUs (24GB VRAM)	Qwen3.8-27B or Qwen3-Coder-30B-A3B	Strong single-file generation, debugging, and scripting without cloud API costs.

Lightweight Hardware (8GB–12GB VRAM)	Qwen2.5-Coder (7B or 14B)	Best suited for autocomplete, boilerplate, and isolated scripts rather than architectural design.

If you are designing a system from scratch or refactoring a complex microservice architecture, 
stick to the Max or Plus API tiers. For daily feature implementation, bug fixes, and local agentic coding, 
the Qwen3-Coder or 27B/30B open-weight models offer strong performance. 

[1] (https://www.yottalabs.ai/post/qwen-4-release-date-what-is-known-how-to-prepare-2026), 
[2] (https://qwen.ai/blog?id=qwen3.8), 
[3] (https://macaron.im/blog/is-qwen-3-5-good-for-coding), 
[4] (https://www.promptquorum.com/prompt-bites/best-qwen-model-for-coding)

---