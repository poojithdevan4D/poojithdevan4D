# Hi, I'm Poojith Devan 👋

**I make LLMs run fast and cheap on hardware you can actually afford.**

Applied inference & performance engineering — serving, quantization, and benchmarking,
built and measured on a **4 GB laptop GPU (RTX 3050)** and cloud T4s, not rented H100s.

🔭 **Now:** shipping applied-inference projects in public (below) · Edge AI Intern @ **OneBit**
(1.58-bit ternary inference) · Research Intern @ **Trebuchet** (Q1.15 fixed-point inference)

---

### 🚀 Applied inference projects — built, measured, deployed

- **[vllm-benchmark](https://github.com/poojithdevan4D/vllm-benchmark)** —
  **vLLM** on a T4: continuous-batching throughput scaled to **~790 tok/s at batch 64** (~7× a GGUF
  backend's peak), and kept rising where the GGUF backend's throughput dropped.
- **[llm-gateway](https://github.com/poojithdevan4D/llm-gateway)** —
  OpenAI-compatible gateway with **health-based failover** (local + cloud), a **semantic cache**
  (embeddings) that serves similar queries without a model call, per-key rate limiting, and graceful degradation.
- **[llm-inference-services](https://github.com/poojithdevan4D/llm-inference-services)** —
  OpenAI-compatible microservice serving a local GPU model *or* a cloud backend from the **same code** — deployed **live**.
- **[serving-benchmark](https://github.com/poojithdevan4D/serving-benchmark)** —
  async load test of the throughput-vs-latency tradeoff. Throughput peaks at **~113 tok/s @ concurrency 4**; past that, tail latency degrades ~5×.
- **[quantization-tradeoff](https://github.com/poojithdevan4D/quantization-tradeoff)** —
  size / speed / quality across Q4 / Q8 / FP16. **Q4_K_M: 3.3× throughput at 1/3 the VRAM of FP16, no measurable accuracy loss.**

### 🔬 Research & earlier work — measured, not claimed

| Result | What |
|---|---|
| **44% MMLU** @ 1.58-bit | hybrid ternary/BF16 Qwen 0.8B beating full-precision 0.5B & 1B baselines — *Cloe v1*, co-authored @ OneBit |
| **77.71%** CIFAR-10, zero float32 leakage | Q1.15 true-integer inference for FPU-less hardware @ Trebuchet |
| **6.5×** throughput · **67%** less VRAM | [QwenQuant](https://github.com/poojithdevan4D/QwenQuant) — llama.cpp Q4_K_M vs FP16 (caught a tokenizer measurement bug) |
| **byte-for-byte** correct | [speculative decoding](https://github.com/poojithdevan4D/qwen-speculative-decoding) from scratch — Qwen2.5-1.5B + 0.5B draft on one 4 GB GPU |

---

### 🛠️ Stack

**Serving:** FastAPI · Docker · Ollama · **vLLM** · OpenAI-compatible APIs · cloud deploy
**Quantization:** GGUF / K-quants · 1.58-bit ternary · Q1.15 fixed-point · INT4 NF4 · INT8 · KV-cache quant
**Perf & infra:** TTFT / throughput / percentiles · semantic caching (embeddings) · routing & failover · rate limiting · Nsight
**Core:** Python · PyTorch · HuggingFace · httpx · matplotlib · CUDA C *(learning)*

---

📫 **poojithdevan@gmail.com** · [LinkedIn](https://www.linkedin.com/in/poojith-devan) · building in public, one project at a time
