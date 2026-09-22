# Qwen

[Qwen3.8 27B is something else.. Caleb Writes Code](https://www.youtube.com/watch?v=3WbXyUolFA0)  

[Is Qwen 3.8 27b The New King of the Local LLMs? Gary Explains](https://www.youtube.com/watch?v=An4_SCFo5-A&t=61s) 

---

# Which of the Qwen model could I run on a Windows 11 PC with 64 GB of RAM shared with the graphic card?

With 64 GB of system RAM shared with an integrated graphics card on a Windows 11 PC (such as an AMD Ryzen AI APU or Intel Core Ultra), 
your computer functions similarly to a unified memory system. While Windows dynamically allocates about half of your system memory (~32 GB) 
as "Shared GPU Memory" by default, modern local AI runners can tap into your full RAM pool using CPU/GPU offloading.

You can comfortably and efficiently run any Qwen model up to the 32B/35B size tier, while 72B models will fit but run painfully slow.

------------------------------

## 🟢 The "Sweet Spot" (Fast & Highly Capable)

These models fit entirely into your RAM with plenty of headroom for Windows 11, background apps, and a large context window. 
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

Qwen models span a broad spectrum of sizes, ranging from ultra-small 0.5B-0.8B variants for mobile devices 
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