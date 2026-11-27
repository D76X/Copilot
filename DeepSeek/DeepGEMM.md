# DeepGEMM

[DeepGEMM - GitHub](https://github.com/deepseek-ai/DeepGEMM)  

[Wird dein lokaler KI Server bald günstiger? Daniel Klozbücher](https://www.youtube.com/watch?v=gF-BT81kpWw)  
[DeepGEMM Explained: The Secret Behind DeepSeek's AI Speed AI Study Group](https://www.youtube.com/watch?v=RAh9ef4UbUo)  

---

# What is DeepGEMM and what problems does it address and solve?

DeepGEMM is an open-source, high-performance GPU kernel library developed by DeepSeek to accelerate General Matrix Multiplication (GEMM) 
and core tensor operations for large language models (LLMs). Originally released in `February 2025` as an `FP8 GEMM library for DeepSeek-V3 and R1`, 
it has evolved into a unified tensor core library supporting: 

- NVIDIA Hopper (SM90), 
- Blackwell (SM100), and 
- Huawei Ascend hardware. 

[1] (https://alphasignal.ai/repo/deepseek-s-deepgemm-fuses-entire-ai-expert-layers-into-one-gpu-operation), 
[2] (https://github.com/deepseek-ai/DeepGEMM?ref=explainx), 
[3] (https://ai.miraheze.org/wiki/DeepGEMM)

Core Problems DeepGEMM Addresses and Solves

• Low-Precision Numerical Instability. Running matrix multiplications in low-bit formats like FP8 and FP4 boosts speed and cuts memory usage, but standard tensor cores suffer from accumulation inaccuracy. DeepGEMM solves this by combining fine-grained block scaling with CUDA-core two-level accumulation (promotion), maintaining high model accuracy without sacrificing throughput. [1] (https://github.com/fengyenet/DEEPSEEK-DeepGEMM), [2] (https://www.youtube.com/watch?v=0hEJg0YhUtU), [3] (https://medium.com/@ashlyajith619/deepgemm-unlocking-the-efficient-fp8-gemm-library-a5d7188c251b)
• Inefficiencies in Mixture-of-Experts (MoE) Routing. Standard GPU libraries like cuBLAS are tuned for static, large square matrices, whereas MoE models constantly route varying numbers of tokens to different experts. DeepGEMM uses specialized grouped GEMMs with contiguous memory layouts and dynamic masking to skip inactive experts, significantly improving memory bandwidth and throughput over generic libraries. [1] (https://www.spheron.network/blog/deploy-deepep-deepgemm-moe-inference-kernels-gpu-cloud/), [2] (https://medium.com/@ashlyajith619/deepgemm-unlocking-the-efficient-fp8-gemm-library-a5d7188c251b)
• Kernel Launch and Communication Bottlenecks. Executing separate GPU kernels for expert routing, linear projections, activations, and inter-GPU communication introduces heavy latency. DeepGEMM introduces fused mega-kernels—such as Mega MoE—that combine dispatch, computation, SwiGLU activation, and combine steps into a single execution flow, overlapping NVLink communication directly with tensor core compute. [1] (https://github.com/deepseek-ai/DeepGEMM?ref=explainx), [2] (https://ai.miraheze.org/wiki/DeepGEMM)
• Heavy Build Times and Codebase Complexity. Traditional GPU kernel libraries like NVIDIA CUTLASS rely on massive, deeply nested C++ templates that take a long time to compile and are difficult to customize. DeepGEMM keeps its core kernel logic concise and uses a lightweight runtime Just-In-Time (DeepJIT) compiler, eliminating compilation during installation while dynamically optimizing kernels for exact matrix shapes. [1] (https://ai.miraheze.org/wiki/DeepGEMM), [2] (https://github.com/deepseek-ai/DeepGEMM?ref=explainx), [3] (https://www.spheron.network/blog/deploy-deepep-deepgemm-moe-inference-kernels-gpu-cloud/)
• Hardware Ecosystem Lock-In. Switching AI workloads between different accelerator families typically requires rewriting low-level GPU code. Through the DeepGEMM-Ascend port, DeepSeek provides an API-compatible backend for Huawei Ascend chips, allowing developers to run the same high-efficiency GEMM and MoE workloads across both NVIDIA and Ascend hardware without changing their application code. [1] (https://www.mindstudio.ai/blog/deepseek-huawei-cuda-alternative), [2] (https://github.com/deepseek-ai/DeepGEMM-Ascend/blob/main/README.md)

---