# Poojith Devan

**LLM inference deployment.** I work on choosing a quantization and serving
configuration for a model, then proving by measurement whether it meets the
latency, memory and quality budget it has to live inside.

Most of that work happens under real hardware constraints rather than on rented
H100s: a 12 GB consumer GPU, free-tier T4s, a 4 GB laptop card. Constraints are
the point. They are what force an actual architecture decision instead of
throwing a bigger instance at the problem.

Research Intern at **OneBit** (1.58-bit ternary inference) and **Trebuchet
System** (Q1.15 fixed-point inference for FPU-less hardware).

Co-author on four papers, two on arXiv and one under review at IEEE TPAMI.

---

## What I have measured

**[vllm-benchmark](https://github.com/poojithdevan4D/vllm-benchmark)** ·
*vLLM, NVIDIA T4, load testing*
Quantifies when continuous batching is worth a migration. vLLM reached **~790
tok/s at batch 64, about 7x a GGUF backend's peak**, and was still scaling where
GGUF had already turned over.

**[serving-benchmark](https://github.com/poojithdevan4D/serving-benchmark)** ·
*async load generation, concurrency sweep*
The sizing curve a deployment actually needs. Throughput peaks near **113 tok/s
at concurrency 4**; past that, p99 latency climbs about **5x** for no throughput
gain. Useful for setting a concurrency cap rather than discovering it in prod.

**[quantization-tradeoff](https://github.com/poojithdevan4D/quantization-tradeoff)** ·
*llama.cpp, Q4 / Q8 / FP16*
The accuracy-versus-cost evidence behind a quantization recommendation.
**Q4_K_M gave 3.3x throughput at one third the VRAM of FP16, with no measurable
accuracy loss** on Qwen2.5-1.5B. An earlier run had made Q4_K_M look 75% worse;
the cause was a tokenizer measurement bug, and finding it reversed the
conclusion. I now benchmark A/B interleaved in one process as standard practice.

**[llm-gateway](https://github.com/poojithdevan4D/llm-gateway)** ·
*FastAPI, Docker, OpenAI-compatible*
A production-shaped serving front end: health-based failover across local and
cloud backends, per-key rate limiting, and an embedding-based semantic cache
that serves similar queries with no model call. Degrades gracefully when the
cache backend is unavailable, so a dependency outage costs latency rather than
availability.

**[llm-inference-services](https://github.com/poojithdevan4D/llm-inference-services)** ·
*deployed*
One OpenAI-compatible codebase serving either a local GPU model or a cloud
backend, so the same client works across deployment targets.

---

## Research

- **Post-Training Ternarization of Qwen3-4B** ([arXiv:2609.01962](https://arxiv.org/abs/2609.01962))
  My contribution: the lossless weight-packing path, 8.29 to 3.96 GiB at 1.641
  effective bits per weight, and the storage and bit-budget accounting.
- **Capability-Stratified Degradation in Ternary Language Models** ([arXiv:2608.28809](https://arxiv.org/abs/2608.28809))
  My contribution: the evaluation harness and the chance-corrected scoring that
  replaced biased default metrics. Chance correction mattered: it is what
  separates a model that has retained a capability from one that is guessing.
- **SuperFloat** (under review, IEEE TPAMI) and **Cloe** (OneBit technical report).

**Ternary inference kernels (OneBit).** Made an 8B model deployable on a single
12 GB consumer GPU instead of a 24 GB card, via a Triton kernel that multiplies
directly against packed ternary weights. Decode **1.48 to 15.5 tok/s**, VRAM
**15.3 to 7.4 GiB**, gated at 100% argmax agreement with the reference before
any speedup was claimed. Then I benchmarked the format against 4-bit NF4 on the
same GPU and recommended **against our own format**: NF4 was faster, smaller and
more accurate. That result is the one I am most glad I published.

**Q1.15 fixed-point inference (Trebuchet).** Qualified a network for hardware
with no floating-point unit: a true-integer forward pass proven at zero float32
leakage by per-operation audit, holding **77.71% CIFAR-10 on ResNet-20**.

**Speculative decoding from scratch.** Qwen2.5-1.5B with a 0.5B draft model on a
single 4 GB GPU, verified byte-for-byte against greedy decoding.

---

## Stack

**Inference and serving** vLLM (continuous batching, concurrency sweeps),
llama.cpp / GGUF, Ollama, FastAPI, Docker, OpenAI-compatible APIs, routing,
health-based failover, semantic caching

**Quantization** GGUF / K-quants, INT4 (NF4, AWQ), INT8, KV-cache quant,
1.58-bit ternary, Q1.15 fixed-point

**Deployment sizing** VRAM budgeting and residency profiling, accuracy-versus-cost
tradeoff analysis, hardware-tier fit, capacity and concurrency limits

**Benchmarking** TTFT, throughput, p50 / p95 / p99 under load, CUDA-event
timing, interleaved A/B methodology, chance-corrected quality retention

**GPU and kernels** Triton kernel authoring, CUDA graphs, Nsight Compute
profiling, roofline analysis. Reading and debugging CUDA C; writing it is in
progress.

**Core** Python, PyTorch, HuggingFace, Git, Linux

---

poojithdevan@gmail.com · [linkedin.com/in/poojith-devan](https://linkedin.com/in/poojith-devan)
