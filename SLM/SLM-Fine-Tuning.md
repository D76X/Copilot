# Fine Tuning by Krish Naik

[Fine Tuning LLM Models – Generative AI Course freeCodeCamp.org](https://www.youtube.com/watch?v=iOdFUJiB0Zc)

[LLM Fine-Tuning Course – From Supervised FT to RLHF, LoRA, and Multimodal freeCodeCamp.org](https://www.youtube.com/watch?v=CcrC5zSv1iA)  

[Finetuning LLM by Krish Naik](https://www.youtube.com/playlist?list=PLZoTAELRMXVN9VbAx5I2VvloTtYmlApe3)  

[Is Fine-Tuning Still Needed? LLMs, RAG, & LoRA IBM Technology](https://www.youtube.com/watch?v=-W2JdSl1v48)  

---

# Gemma 4 Fine-Tuning

[Gemma 4 Fine-Tuning on Single GPU | Training Gemma 4 With Unsloth on Custom Dataset Venelin Valkov](https://www.youtube.com/watch?v=wb6UGP2PgCU)   

---

# Is it expensive to fine tune gemma 4?

Fine-tuning Gemma 4 is not expensive, and costs range from $0 (free) to around $50–$500, 
depending on the model size and hardware you use. 

[1] (https://wavect.io/blog/fine-tune-gemma-4-free-unsloth-colab/), 
[2] (https://aicostcheck.com/blog/google-gemma-4-cost-analysis-open-model-2026)

## Cost Breakdown by Approach

- Free / Local Hardware (0.00 USD):
	You can fine-tune smaller variants (like Gemma 4 E2B or E4B) completely free using Unsloth 
	on a free Google Colab tier or locally on consumer GPUs with as little as 8GB to 12GB of VRAM 
	(such as an RTX 3060 or RTX 4090). 
	
	[1] (https://cloudinsight.cc/en/blog/gemma-4-fine-tuning), 
	[2] (https://medium.com/ai-by-design/fine-tuning-gemma-4-on-a-single-gpu-a-production-qlora-walkthrough-11d1df8fc7f4), 
	[3] (https://www.reddit.com/r/unsloth/comments/1sewq4t/you_can_now_finetune_gemma_4_locally_8gb_vram/), 
	[4] (https://wavect.io/blog/fine-tune-gemma-4-free-unsloth-colab/)

- Budget Cloud GPU Runs ($0.38 – $11.00 USD):
	Quick experimental runs or training on cloud platforms (like `VESSL Cloud` or `RunPod` with an A100 or RTX 3090) 
	typically cost under a dollar to about $11.00 for smaller-to-medium fine-tuning sessions. 
	
	[1] (https://vessl.ai/en/blog/fine-tune-gemma-4-on-cloud-gpu), 
	[2] (https://medium.com/autocomplete-real-world-ai/i-fine-tuned-gemma-4-to-sound-like-me-7f45a8a576f3), 
	[3] (https://dev.to/rukshanjs/i-fine-tuned-gemma-4-for-latex-ocr-the-success-was-the-problem-4ehi)

- Larger Models ($50 – $500+ USD):
	Fine-tuning `larger dense` or `mixture-of-experts (MoE)` variants like the `Gemma 4 31B model` 
	using `Parameter-Efficient Fine-Tuning (PEFT/LoRA)` generally runs between $50 and $500 in total 
	GPU compute time. 
	
	[1] (https://aicostcheck.com/blog/google-gemma-4-cost-analysis-open-model-2026)

## Why It Is Affordable

- `PEFT / QLoRA Support`: 
You do not need an expensive cluster of H100 or A100 GPUs. Techniques like `QLoRA` 
reduce the VRAM footprint significantly (e.g., dropping 31B model memory requirements down to ~22GB), 
allowing training on single consumer-grade or mid-tier cloud GPUs. 

[1] (https://cloudinsight.cc/en/blog/gemma-4-fine-tuning)

- `Permissive Licensing`: 
`Gemma 4` is released under the `Apache 2.0 license`, meaning there are zero ongoing licensing fees, 
no monthly active user (MAU) limits, and full freedom for commercial deployment after fine-tuning. 

[1] (https://aitoolbrief.io/blog/google-gemma-4-review-2026-features-benchmarks-pricing-how-to-use-it), 
[2] (https://aicostcheck.com/blog/google-gemma-4-cost-analysis-open-model-2026)

---

# Fine-tuning in Azure

[Fine-tune a model with supervised fine-tuning in Microsoft Foundry](https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/fine-tuning?tabs=foundry-sdk&pivots=programming-language-studio)  

Here is a video demonstrating how to perform fine-tuning and model customization within Azure AI Foundry:
[Fine-Tune LLM Models with Ease on Azure AI Foundry Tech with Kirk](https://www.youtube.com/watch?v=dQLG34PjjSQ)  

---

Fine-tuning in Azure is managed primarily through Microsoft Foundry (formerly Azure AI Foundry / Azure AI Studio) 
and Azure OpenAI Service, allowing you to customize pre-trained foundation models (such as GPT-4o-mini, GPT-4o, 
or open-source models like Llama) on your own task-specific data. 

[1] (https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/fine-tuning), 
[2] (https://learn.microsoft.com/en-us/azure/foundry-classic/concepts/fine-tuning-overview), 
[3] (https://azure.microsoft.com/en-us/blog/announcing-new-fine-tuning-models-and-techniques-in-azure-ai-foundry/)

## Core Fine-Tuning Approaches in Azure

- `Supervised Fine-Tuning (SFT)`: 
Trains a model using pairs of prompts and desired responses to adapt its 
style, tone, formatting, or task behavior. 

[1] (https://learn.microsoft.com/en-us/azure/foundry/fine-tuning/overview), 
[2] (https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/fine-tuning)

- `Preference Fine-Tuning (e.g., DPO)`: 
Optimizes model outputs based on preferred vs. rejected responses to align with quality and tone preferences. 

[1] (https://learn.microsoft.com/en-us/azure/foundry/fine-tuning/overview)

- `Reinforcement Fine-Tuning (RFT)`: 
Uses automated graders or custom logic to score generated outputs for complex reasoning and decision-making tasks 
(e.g., for models like o4-mini). 

[1] (https://azure.microsoft.com/en-us/blog/announcing-new-fine-tuning-models-and-techniques-in-azure-ai-foundry/), 
[2] (https://learn.microsoft.com/en-us/azure/foundry/fine-tuning/overview)

- `Managed vs. Serverless vs. Compute`:
	
	- `Serverless/Managed Training`: Foundry runs the training infrastructure for you without needing to provision dedicated GPUs.
	
	- `Managed Compute / Azure Kubernetes Service (AKS)`: Uses KAITO or custom VMs if you need full control over open-source model training and infrastructure. 
	
	[1] (https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models), 
	[2] (https://learn.microsoft.com/en-us/azure/foundry-classic/concepts/fine-tuning-overview), 
	[3] (https://learn.microsoft.com/en-us/azure/foundry/fine-tuning/overview)

## How to Get Started

You can run fine-tuning jobs using: 

- `the Microsoft Foundry Fine-Tuning Guide`, 
- the Azure AI Python SDK (azure-ai-projects / openai), or 
- the Azure Developer CLI (azd): 

[1] (https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/fine-tuning)

1. Prepare Data: Gather high-quality training and validation examples (starting with 50–100 examples for testing, scaling to 500+ for production).

2. Configure the Job: Select your base model, set hyperparameters (such as epochs and batch size), and specify your project endpoint.

3. Deploy and Monitor: Track training progress in Foundry, deploy the resulting custom model endpoint, and monitor usage. 

[1] (https://learn.microsoft.com/en-us/azure/foundry-classic/openai/tutorials/fine-tune), 
[2] (https://learn.microsoft.com/en-us/azure/foundry-classic/concepts/fine-tuning-overview), 
[3] (https://learn.microsoft.com/en-us/azure/foundry/openai/how-to/fine-tuning), 
[4] (https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/retrieval-augmented-fine-tuning-use-gpt-4o-to-fine-tune-gpt-4o-mini-for-domain-s/4248861)

> Note: 

Deployed fine-tuned models incur hourly hosting costs in addition to token usage, and 
deployments inactive for more than 15 days are automatically removed (though the underlying model remains saved). 

[1] (https://learn.microsoft.com/en-us/azure/foundry-classic/openai/tutorials/fine-tune)

---




