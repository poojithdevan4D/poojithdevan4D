**Applied inference & performance engineering.** I work on making LLMs run fast and cheap on hardware
most people can actually afford — serving, quantization, and benchmarking, mostly on a 4 GB laptop GPU
and free cloud T4s rather than rented H100s.

Right now I'm an Edge AI Intern at OneBit (1.58-bit ternary inference) and a Research Intern at
Trebuchet (Q1.15 fixed-point inference).

## Projects

**[vllm-benchmark](https://github.com/poojithdevan4D/vllm-benchmark)** — Benchmarked vLLM on a T4.
Continuous-batching throughput scaled to ~790 tok/s at batch 64, roughly 7× a GGUF backend's peak,
and kept climbing where the GGUF backend tailed off.

**[llm-gateway](https://github.com/poojithdevan4D/llm-gateway)** — An OpenAI-compatible gateway with
health-based failover across local and cloud backends, a semantic cache that answers similar
questions without calling a model, per-key rate limiting, and graceful degradation when the cache
is unavailable.

**[llm-inference-services](https://github.com/poojithdevan4D/llm-inference-services)** — An
OpenAI-compatible microservice that serves a local GPU model or a cloud backend from the same code,
deployed live.

**[serving-benchmark](https://github.com/poojithdevan4D/serving-benchmark)** — An async load test of
the throughput-vs-latency tradeoff. Throughput peaks around 113 tok/s at concurrency 4; beyond that,
tail latency climbs about 5× for no real gain.

**[quantization-tradeoff](https://github.com/poojithdevan4D/quantization-tradeoff)** — Size, speed,
and quality across Q4/Q8/FP16. Q4_K_M ran 3.3× faster at a third of the VRAM of FP16, with no
measurable accuracy loss on my eval.

## Research and earlier work

- **Cloe v1** (co-authored at OneBit) — a hybrid ternary/BF16 Qwen 0.8B reached 44% MMLU, beating
  full-precision 0.5B and 1B baselines.
- **Q1.15 fixed-point inference** (Trebuchet) — a true-integer forward pass with zero float32
  leakage; 77.71% CIFAR-10 on ResNet-20.
- **[QwenQuant](https://github.com/poojithdevan4D/QwenQuant)** — a 4-way quantization benchmark where
  I caught a tokenizer measurement bug that had made Q4_K_M look 75% worse than it actually was.
- **[Speculative decoding from scratch](https://github.com/poojithdevan4D/qwen-speculative-decoding)**
  — Qwen2.5-1.5B with a 0.5B draft model on a single 4 GB GPU, verified byte-for-byte against greedy
  decoding.

## Stack

- **Serving:** FastAPI, Docker, Ollama, vLLM, OpenAI-compatible APIs
- **Quantization:** GGUF / K-quants, 1.58-bit ternary, Q1.15 fixed-point, INT4 / INT8, KV-cache quant
- **Performance & infra:** throughput/latency benchmarking, semantic caching, routing & failover, rate limiting
- **Core:** Python, PyTorch, HuggingFace, httpx, matplotlib. Currently learning CUDA C.

---

poojithdevan@gmail.com · [linkedin.com/in/poojith-devan](https://www.linkedin.com/in/poojith-devan)
