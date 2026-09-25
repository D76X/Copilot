# LLMs FAQ

---

# What is an open-weight model, and how does it differ from other types of models?

An **open-weight model** is an artificial intelligence model whose trained numerical parameters—known as **weights**—are made publicly available for anyone to download, 
inspect, host, and run locally or on their own infrastructure.

While you can run open-weight models on your own hardware, you cannot necessarily recreate them from scratch, as the raw training data, preprocessing pipelines, and supercomputing code used to build them may remain proprietary.

---

## How Open-Weight Compares to Other Model Types

AI models generally fall along a spectrum of transparency and control, ranging 
from fully proprietary to fully open source:

| Dimension | **Closed-Source / Closed-Weight** | **Open-Weight** | **Fully Open-Source (Open AI Ecosystem)** |
| --- | --- | --- | --- |
| **Examples** | OpenAI GPT-4o, Anthropic Claude 3.5, Google Gemini | Meta Llama 3, Mistral 7B, Alibaba Qwen 2.5 | Allen AI OLMo, EleutherAI Pythia |
| **Model Weights** | Hidden (API access only) | **Publicly downloadable** | **Publicly downloadable** |
| **Source Code & Data** | Private | Often partial (code released, dataset private) | Fully public (weights, training data, code, docs) |
| **Where It Runs** | Host's cloud servers only | Locally, on private clouds, or vendor servers | Anywhere |
| **Customization** | System prompts, fine-tuning via vendor API | Full control: fine-tuning, quantization, modification | Full control: retrain, modify architecture, fine-tune |
| **Privacy & Security** | Data sent to third-party vendor APIs | Data stays on your own infrastructure | Data stays on your own infrastructure |

---

## Key Advantages & Limitations

### **Advantages of Open-Weight Models**

* **Data Privacy & Compliance:** Because the weights run on your own hardware or VPC, sensitive data never leaves your controlled environment.

* **Cost Efficiency at Scale:** Avoids per-token API pricing models when handling high-volume workloads.

* **Customizability & Control:** Models can be fine-tuned via techniques like LoRA or QLoRA on domain-specific datasets, quantized to run on lower-spec hardware, or integrated directly into custom local tools via frameworks like `Ollama`, `vLLM`, or the Model Context Protocol (MCP).

* **No Vendor Lock-In:** You control the hosting, versioning, and availability without risk of sudden deprecation or policy changes by an external API provider.

### **Limitations & Considerations**

* **Hardware Requirements:** Running larger models (e.g., 70B+ parameters) with high throughput requires substantial GPU VRAM and infrastructure setup.

* **The "Open Source" Distinction:** True open source requires open access to the software *and* training materials (per OSI definitions). Many open-weight licenses restrict commercial usage above certain thresholds or withhold the underlying training data.

* **Maintenance & Security:** Hosting open-weight models places responsibility for latency, scaling, safety alignment, and infrastructure security entirely on your team.

---