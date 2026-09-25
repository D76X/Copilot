# Qwen3.8-27B Local Deployment Analysis

**Assessment date:** 25 September 2026  
**Target PC:** Dell Precision 3590, Windows 11 Enterprise  
**Decision:** Proceed with a controlled Ollama pilot. Qwen3.8-27B fits on disk and in system RAM at 4-bit quantization, but it will run mostly on the CPU because the NVIDIA GPU has only 4 GB of dedicated VRAM. Keep Gemma 4 and Qwen3.8 on disk, but normally load and use only one at a time.

## Executive answer

Yes, the intended setup is feasible:

- Keep `gemma4:latest` and `qwen3.8:27b` installed together. Stored model files consume disk, not working RAM.
- Select Gemma for faster, lighter work and Qwen3.8-27B for harder coding and agentic tasks.
- Stop or allow Ollama to unload one model before loading the other. The models do not each reserve RAM merely because they are installed.
- Expect Qwen3.8-27B to fit, but not to be fast like it would be on a 24-32 GB VRAM desktop GPU. This laptop's 4 GB NVIDIA GPU can offload only a small part of the model.
- Do not start with the advertised 256K context. Begin at 16K, test 32K, and attempt 64K only after measuring memory and speed with other large applications closed.

The main correction to the collected notes is the phrase "64 GB of RAM shared with the graphic card." This PC does not have Apple-style unified memory. It has 64 GB of system RAM, an NVIDIA discrete GPU with 4 GB of dedicated VRAM, and an Intel integrated GPU. Windows may report shared GPU memory, but that is ordinary system RAM reached through a slower path; it is not equivalent to adding VRAM. The current Ollama CUDA path uses the NVIDIA GPU and system-RAM/CPU offload.

## Direct answers to the questions

| Question | Answer |
|---|---|
| Which graphics card is installed? | NVIDIA RTX 500 Ada Generation Laptop GPU, Ada Lovelace, 4,094 MiB dedicated VRAM, plus Intel Arc integrated graphics. |
| Is it good for local coding LLMs? | It is supported and useful as a small accelerator, but 4 GB VRAM is entry-level for LLM inference. It is far below the 16-32 GB VRAM class that can hold a 27B Q4 model largely or wholly on the GPU. |
| Is 64 GB RAM enough for Qwen3.8-27B? | Yes for the official Ollama Q4_K_M package at a modest context. It is not enough to treat 256K context as free, especially while many applications are open. |
| Is there enough disk space? | Yes. The PC had 441.8 GiB free. The Ollama Qwen package is 18 GB; Gemma currently uses 9.6 GB according to `ollama list`. |
| Can both models remain installed? | Yes. Together they require about 27.6 GB of model storage, plus small metadata and possible download/cache overhead. |
| Can one be used for easy work and the other for coding? | Yes. This is the recommended arrangement. Model selection is per Ollama command or API request. |
| Do both consume RAM while merely stored? | No. They consume substantial RAM/VRAM only while loaded. Ollama normally keeps a used model loaded for five minutes, or it can be unloaded immediately with `ollama stop <model>`. |
| Should both be loaded concurrently? | No for this PC. It may be technically possible at small contexts, but it wastes scarce memory and offers no advantage for the intended one-model-at-a-time workflow. |

## What is actually installed and measured

### Hardware inventory

| Component | Measured value | Relevance |
|---|---:|---|
| Computer | Dell Precision 3590 | Mobile workstation; GPU power and cooling are laptop-constrained. |
| OS | Windows 11 Enterprise, 64-bit | Native Ollama Windows installation is supported. |
| CPU | Intel Core Ultra 7 165H, 16 cores / 22 logical processors | Capable mobile CPU, but 27B generation will be constrained mainly by memory bandwidth. |
| RAM | 63.46 GiB usable, 2 x 32 GB DDR5, configured at 4,800 MT/s | Sufficient for Qwen3.8 Q4 with a controlled context. Dual modules are helpful for CPU inference bandwidth. |
| Free RAM during audit | 32.71 GiB | Roughly 30.75 GiB was already in use. Close browsers, IDE instances, Docker workloads, or VMs before a long-context Qwen run. |
| NVIDIA GPU | RTX 500 Ada Generation Laptop GPU | CUDA-supported Ada GPU. |
| NVIDIA VRAM | 4,094 MiB, about 3.8 GiB usable after reservation | Too small to hold the 17 GB language-model weights. Most layers must remain in system RAM. |
| NVIDIA power limit | 25 W current, 30 W default, 35 W maximum reported | Another indication that this is a low-power mobile GPU, not a high-throughput LLM GPU. Do not change power settings merely for this pilot. |
| Integrated GPU | Intel Arc Graphics | Can use shared system memory, but the observed Ollama run selected the NVIDIA CUDA backend. It does not turn the machine into a unified-memory GPU system. |
| SSD | 1 TB Micron NVMe | Suitable model storage. |
| Free disk | 441.8 GiB on `C:` | More than enough for both models and temporary download overhead. |
| Page file | 22 GiB allocated | Emergency headroom only. Sustained paging would make inference unacceptably slow and should count as a failed configuration. |

### Existing Ollama and Gemma baseline

- Ollama version: `0.34.4`.
- Installed model: `gemma4:latest`.
- Gemma metadata: 8.0B parameters, Q4_K_M, 131,072-token model context.
- Gemma storage reported by Ollama: 9.6 GB; `.ollama\models` occupied 8.95 GiB on disk because GB and GiB use different units.
- When loaded, `ollama ps` reported a 10 GB allocation split as **86% CPU / 14% GPU** at 131,072 context.
- NVIDIA VRAM use reached about 2,451 MiB.
- Ollama's log reported only **1 of 43 layers** offloaded to the GPU and `n_ctx = 131072`.
- A single 160-token baseline generated at 10.33 tokens/s, processed the small prompt at 33.43 tokens/s, and took 14.77 seconds to load. This is a baseline observation, not a formal benchmark.

This measured Gemma behavior is the strongest evidence about Qwen on this PC: even an 8B model is predominantly CPU-backed. Qwen's 27.3B model is much larger and should be expected to generate materially more slowly.

## The exact Qwen model under consideration

The model name is valid and current. The canonical sources identify it as `Qwen/Qwen3.8-27B`, and Ollama exposes it as:

```powershell
qwen3.8:27b
```

The official Ollama artifact contains:

| Part | Details |
|---|---|
| Language model | 27.3B parameters, Q4_K_M, approximately 17 GB |
| Vision projector | 461M parameters, BF16, approximately 931 MB |
| Complete Ollama package | 18 GB |
| Native model context | 262,144 tokens; Ollama displays 256K |
| Inputs/capabilities | Text and images; thinking and tool support |
| License | Apache-2.0 |

Qwen describes this as a **dense** 27B vision-language model built on the Qwen3.5 architecture, with improvements in coding, professional work, research, long-horizon agentic tasks, planning, and handling tool/environment feedback. Its model card includes agentic-terminal coding, SWE-bench Pro, repository-level generation, DeepSWE, QwenSWEBench, and LiveCodeBench evaluations.

Those benchmark claims support a coding pilot, but they do not guarantee the same outcome here. The official coding evaluations commonly use a Claude Code harness, 256K context, long timeouts, and the unquantized/reference model environment. A local Q4_K_M build at 16K-32K context on a CPU-dominant laptop must be evaluated separately.

## Capacity analysis

### Disk

| State | Approximate model storage |
|---|---:|
| Gemma only, current | 9.6 GB reported by Ollama |
| Qwen3.8-27B package | 18 GB |
| Both retained | 27.6 GB plus small manifests/cache |
| Free space before Qwen | 441.8 GiB |

Disk is not a constraint. Even allowing another full package's worth of temporary download space, the SSD has ample capacity.

### RAM and VRAM

The statement "Qwen costs at least 20 GB of RAM" is a useful rough intuition, not a fixed reservation:

1. The stored Q4 weights/projector total 18 GB.
2. Runtime structures, model metadata, compute buffers, and the context cache add memory.
3. A portion can be offloaded to the 4 GB NVIDIA GPU, but most will remain in system RAM.
4. Context length and concurrent requests can change memory use dramatically.

For the 16 full-attention layers visible in Qwen's published configuration, an F16 key/value cache is approximately 64 KiB per token before other runtime state. That is roughly:

| Context | Approximate full-attention KV component only |
|---:|---:|
| 4K | 0.25 GiB |
| 16K | 1 GiB |
| 32K | 2 GiB |
| 64K | 4 GiB |
| 256K | 16 GiB |

Qwen also has linear-attention state, vision components, compute buffers, and runtime overhead, so these figures are not total memory estimates. They show why "supports 256K" does not mean "256K is sensible on this machine."

A reasonable planning range for Qwen is approximately **20-25 GiB of combined system RAM/VRAM at 16K-32K context**, with actual allocation to be measured after installation. At the audit's 32.7 GiB free RAM, that should fit with useful headroom. A 64K context may fit after closing memory-heavy applications, but prompt processing and generation will be slower. A 256K allocation is not recommended.

### Expected performance

No honest tokens-per-second result can be given before pulling and running this exact Ollama artifact. A cautious expectation is:

- initial model load noticeably longer than Gemma's measured 14.77 seconds;
- generation substantially below Gemma's measured 10.33 tokens/s;
- approximately 2-5 tokens/s is a planning estimate, not a promise;
- long prompts and thinking mode can make completion latency much longer than the raw generation rate suggests.

The model's hybrid architecture and Ollama's implementation may perform better or worse than a simple 27B/8B size ratio. The pilot benchmark is therefore a required decision gate.

## GPU assessment and comparison

The RTX 500 Ada Laptop GPU is a modern, supported CUDA device, but its **4 GB VRAM and 25-35 W mobile power envelope** make it weak for a 27B local LLM. It can accelerate a small offloaded portion and some prompt processing, but it cannot hold Qwen3.8-27B's 17 GB Q4 language model.

A useful local-LLM comparison is VRAM capacity rather than model-year branding:

| GPU class | Example capacities | Qwen3.8-27B Q4 implication |
|---|---:|---|
| This laptop | RTX 500 Ada Laptop, 4 GB | Mostly CPU/system-RAM inference; slowest class considered here. |
| Mainstream newer laptop | RTX 5060/5050 Laptop, 8 GB | More offload, but still not enough for all 18 GB. |
| Higher-end laptop | RTX 5080 Laptop, 16 GB; RTX 5090 Laptop, 24 GB | 16 GB nearly holds the language weights but not the full package/context; 24 GB can hold the model at modest context and is much more suitable. |
| High-end desktop | RTX 3090/4090, 24 GB; RTX 5090, 32 GB | Appropriate for largely/full GPU-resident 27B Q4 inference, with 32 GB providing better context headroom. |

NVIDIA's current comparison pages list 24 GB for RTX 5090 Laptop, 16 GB for RTX 5080 Laptop, and 32 GB for desktop RTX 5090. They also show far wider desktop memory subsystems. This does not mean a GPU upgrade is required: the existing PC can run Qwen. It means the user experience will be closer to CPU inference than to demonstrations recorded on 24 GB or larger GPUs.

For a future machine specifically geared to local coding models, prioritize:

1. at least 24 GB dedicated VRAM for a 27B Q4 model and modest context;
2. 32 GB VRAM if long context, larger quantization, or more GPU headroom matters;
3. 64 GB or more system RAM;
4. high memory bandwidth and adequate cooling/power, not just CUDA-core count.

An external GPU is generally not an attractive upgrade path for this laptop unless it has a supported high-bandwidth connection and the total enclosure/GPU cost is justified. A desktop with a 24-32 GB card is the cleaner performance upgrade.

## Corrected interpretation of `Local-LLM\Qwen.md`

The notes reached the right broad decision but contain claims that should not drive installation without qualification:

- **Correct:** `qwen3.8:27b` exists, the official Ollama package is Q4_K_M, is coding-oriented, and fits a 64 GB PC.
- **Correct:** both Gemma and Qwen can remain on disk and be selected per task.
- **Needs correction:** 64 GB is not one unified pool shared equally with the NVIDIA GPU. The observed path is 4 GB NVIDIA VRAM plus CPU/system-RAM offload.
- **Needs correction:** "excellent responsiveness" is not established for this laptop. The 4 GB GPU makes Qwen CPU-dominant.
- **Needs correction:** memory is not a fixed 20 or 24 GB. Context, cache precision, vision input, parallel requests, and runtime buffers matter.
- **Needs correction:** reserving 8-16 GB as an Intel UMA frame buffer is not a general performance recommendation here and could reduce RAM available to Ollama. Do not change BIOS memory allocation for the initial pilot.
- **Needs correction:** the 256K native context and optional/hosted 1M capability are model limits, not practical initial settings for this hardware.
- **Unsupported:** the claim that a 4-bit quantization retains "over 99%" of capability is too absolute. Q4_K_M is the sensible capacity/quality compromise, but task-specific quality must be measured.
- **Do not substitute casually:** Qwen3.5-35B-A3B is a different MoE model. It may have fewer active parameters per token, but its Ollama package is 24 GB and it is not the requested Qwen3.8-27B dense model.

The empty `.github\specs\02-spec-qwen3.8.md` supplies no requirements yet. The implementation plan below can serve as the content baseline for a later formal specification, but this report does not silently populate or invent requirements in that file.

## Recommended operating model

### Model roles

| Work type | Preferred model | Reason |
|---|---|---|
| General chat, summaries, short explanations, simple transformations | `gemma4:latest` | Already installed; measured at about 10 tokens/s; lower memory and faster load. |
| Repository reasoning, debugging, multi-file changes, tool use, harder coding | `qwen3.8-coding-16k` initially | Qwen's stated strengths align with these tasks; constrained context avoids waste. |
| Large-repository/long-context coding | Qwen alias at 32K, then possibly 64K | Increase only after measuring RAM, paging, prompt speed, and task quality. |
| Simultaneous serving | Neither combination recommended | Use one model at a time on this PC. |

### Switching models

Models remain installed when stopped:

```powershell
# Switch from Gemma to Qwen
ollama stop gemma4
ollama run qwen3.8-coding-16k

# Switch back to Gemma
ollama stop qwen3.8-coding-16k
ollama run gemma4

# Show what is currently resident
ollama ps

# Show everything retained on disk
ollama list
```

By default, Ollama keeps a recently used model in memory for five minutes. `ollama stop` releases it immediately. For API clients, `keep_alive: 0` unloads after a response; a positive duration retains it for reuse.

## Phased implementation plan

### Phase 0 - Preserve and record the baseline

- Record `ollama --version`, `ollama list`, `ollama ps`, free RAM, free disk, and `nvidia-smi` output.
- Keep `gemma4:latest`; do not remove or overwrite it.
- Stop unused Docker containers, VMs, large browser sessions, and extra IDE instances for the first Qwen test.
- Do not change BIOS GPU-memory settings.

### Phase 1 - Install the official package

1. Update Ollama through its normal Windows updater before pulling this newly released architecture. The current installation is `0.34.4`; use the newest stable build offered by Ollama rather than assuming this version supports every Qwen3.8 path.
2. Confirm at least 25 GB free. The PC currently exceeds this by a wide margin.
3. Pull the explicit model tag:

```powershell
ollama pull qwen3.8:27b
```

4. Verify identity and quantization:

```powershell
ollama show qwen3.8:27b
ollama list
```

Expected facts are approximately 27.3B language-model parameters, Q4_K_M, and an 18 GB package. If Ollama reports an unsupported architecture, update Ollama rather than switching to an unverified community model.

### Phase 2 - Create a conservative coding profile

Create a small `Modelfile` outside the repository unless the configuration is intentionally being version-controlled:

```text
FROM qwen3.8:27b
PARAMETER num_ctx 16384
```

Then create a lightweight alias. Ollama's content-addressed storage should reuse the same model blobs rather than duplicate 18 GB:

```powershell
ollama create qwen3.8-coding-16k -f .\Modelfile
```

Start with 16K because this is large enough for meaningful coding work while establishing a safe baseline. Later aliases can use 32,768 or 65,536 after validation. Do not begin at 262,144.

### Phase 3 - Validate capacity and performance

Run a short prompt, a medium code explanation, and a real but non-destructive repository task. During each test record:

```powershell
ollama ps
nvidia-smi
Get-CimInstance Win32_OperatingSystem |
  Select-Object @{Name='FreeRAMGiB';Expression={[math]::Round($_.FreePhysicalMemory/1MB,2)}}
```

Use Ollama's non-streaming API for reproducible timing because its response includes prompt-evaluation and generation durations. Test the same prompt and output-token limit against Gemma and Qwen.

Provisional go/no-go gates:

| Gate | Pass condition |
|---|---|
| Correct package | `ollama show` reports Qwen3.8 27B and Q4_K_M. |
| Memory safety | No out-of-memory error; no sustained page-file growth; preferably at least 8 GiB free RAM during representative use. |
| Residency | `ollama ps` shows the expected context and a CPU/GPU split; mostly CPU is expected. |
| Interactive speed | At least about 3 output tokens/s is a reasonable subjective target; 1-3 may be acceptable for hard batch tasks; below 1 is unlikely to be pleasant. |
| Coding quality | Qwen gives a material advantage over Gemma on the user's actual debugging, multi-file, and tool-use tasks, not only generic prompts. |
| Reliability | It completes repeated tool calls and tests without loops, invented success, or malformed calls. |

If 16K passes comfortably, repeat at 32K. Test 64K only if memory remains healthy and the larger context solves a demonstrated need. Revert to 16K/32K if paging or prompt latency becomes excessive.

### Phase 4 - Connect to existing interfaces

#### Open WebUI

The existing Open WebUI setup points at the native Windows Ollama endpoint. After the pull, Qwen should appear in the same model selector as Gemma. Keep web search/RAG result counts small at first because retrieved pages consume context quickly.

#### GitHub Copilot CLI

The repository already documents Ollama through Copilot CLI's OpenAI-compatible endpoint. For the Qwen alias, the PowerShell session would use:

```powershell
$env:COPILOT_PROVIDER_TYPE = 'openai'
$env:COPILOT_PROVIDER_BASE_URL = 'http://localhost:11434/v1'
$env:COPILOT_PROVIDER_API_KEY = 'ollama'
$env:COPILOT_MODEL = 'qwen3.8-coding-16k'
$env:COPILOT_OFFLINE = 'true'
copilot
```

`COPILOT_OFFLINE=true` is important when the goal is a local provider. Tool commands can still reach the network if the user explicitly approves and runs network-capable tools; local inference alone does not give the model autonomous Internet access.

Validate simple read-only tool use before allowing broad repository edits. A model can be good at coding benchmarks and still be unreliable with a particular agent harness or a quantized local runtime.

### Phase 5 - Decide whether to retain the pilot

Retain both models if Qwen is measurably better on hard coding tasks and its latency is acceptable. Remove only Qwen if it is too slow:

```powershell
ollama rm qwen3.8-coding-16k
ollama rm qwen3.8:27b
```

Removing the alias alone should not remove shared model blobs still referenced by the base tag. Do not remove `gemma4:latest` unless that is a separate deliberate decision.

## Risks and mitigations

| Risk | Mitigation |
|---|---|
| Qwen fits but is too slow | Benchmark before integrating deeply; reserve it for hard tasks; keep Gemma for routine work. |
| Context setting consumes too much memory | Start at 16K, monitor RAM/page file, and raise incrementally. |
| Ollama version lacks complete support for the new model | Update Ollama first; use the official `qwen3.8:27b` tag. |
| 4-bit quality differs from published results | Compare on representative repository tasks and require tests, not persuasive prose. |
| Thinking mode creates long waits | Use it for hard tasks; disable or reduce reasoning only after checking the current Ollama/Qwen request controls. |
| Both models remain loaded | Use `ollama stop`; leave the default five-minute eviction or set a shorter `keep_alive`. |
| System begins paging | Close other applications, reduce context, reduce parallelism, and treat continued paging as a failed setup. |
| Tool-enabled model makes unsafe changes | Start read-only, use Git, inspect diffs, and require tests. Local does not mean infallible. |
| Advertised 256K encourages over-allocation | Treat 256K as an architectural maximum, not the laptop's operating target. |

## Final recommendation

Install and evaluate the official `qwen3.8:27b` Ollama model. The PC has ample disk and enough 64 GB system RAM for its 18 GB Q4_K_M package at a modest context. Preserve Gemma and use explicit switching: Gemma for routine work, Qwen for harder coding.

The limiting component is the RTX 500 Ada Laptop GPU's 4 GB VRAM, not disk or total RAM. Qwen should run, but mostly through the Core Ultra CPU and DDR5 system memory. The correct expectation is **higher coding capability at lower speed**, not a fast GPU-resident 27B experience. The implementation should proceed only through the staged 16K -> 32K -> optional 64K benchmark plan above.

## Evidence and sources

### Local evidence collected on this PC

- `Get-CimInstance Win32_ComputerSystem`, `Win32_OperatingSystem`, `Win32_Processor`, `Win32_PhysicalMemory`, and `Win32_VideoController`.
- `Get-PhysicalDisk`, `Win32_LogicalDisk`, and `Win32_PageFileUsage`.
- `nvidia-smi` and `nvidia-smi -q`.
- `ollama --version`, `ollama list`, `ollama show gemma4`, `ollama ps`, Ollama `server.log`, and a timed local API generation.
- Repository notes: [`Local-LLM/Qwen.md`](Local-LLM/Qwen.md), [`Local-LLM/Gemma 4.md`](Local-LLM/Gemma%204.md), [`Local-LLM/GitHub Copilot CLI with Local Model.md`](Local-LLM/GitHub%20Copilot%20CLI%20with%20Local%20Model.md), and the empty [`.github/specs/02-spec-qwen3.8.md`](.github/specs/02-spec-qwen3.8.md).

### Web sources

- [Qwen official model card: Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B)
- [Qwen official published configuration](https://huggingface.co/Qwen/Qwen3.8-27B/blob/main/config.json)
- [Ollama official Qwen3.8-27B package](https://ollama.com/library/qwen3.8:27b)
- [Ollama FAQ: storage, unloading, concurrency, GPU/CPU split, and cache quantization](https://docs.ollama.com/faq)
- [Ollama context-length guidance](https://docs.ollama.com/context-length)
- [Ollama Windows requirements and model storage](https://docs.ollama.com/windows)
- [Ollama hardware support](https://docs.ollama.com/gpu)
- [NVIDIA GeForce laptop GPU comparison](https://www.nvidia.com/en-us/geforce/laptops/compare/)
- [NVIDIA desktop GPU comparison](https://www.nvidia.com/en-us/geforce/graphics-cards/compare/)

The three videos listed in `Qwen.md` helped identify the topic, but hardware-fit and installation conclusions in this report rely on direct machine measurements and the official Qwen, Ollama, and NVIDIA sources above.
