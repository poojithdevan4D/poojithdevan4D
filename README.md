# Hi, I'm Poojith Devan 👋

**I make LLMs run fast on hardware you can actually afford.**

Quantization, KV-cache compression, and inference optimization — implemented from
scratch and benchmarked on a **4 GB laptop GPU (RTX 3050)** and **decade-old ARM phones**,
not on rented H100s.

🔭 Currently: **Edge AI Intern @ OneBit** (1.58-bit ternary inference) · **Research Intern @ Trebuchet** (Q1.15 fixed-point inference)

---

### Things I've measured, not just claimed

| Result | What |
|---|---|
| **6.5×** throughput, **67%** less VRAM | llama.cpp Q4_K_M vs FP16 on a 4 GB RTX 3050 |
| **2.5×** faster | hand-written ARM NEON INT8 kernels on a 2013 Cortex-A9 phone |
| **5.3×** smaller KV cache | 3-bit KV-cache quantization, ~80% top-5 recall kept |
| **byte-for-byte** correct | speculative decoding implemented from scratch vs greedy decoding |
| **44% MMLU** @ 1.58-bit | hybrid ternary/BF16 Qwen 0.8B beating FP 0.5B & 1B baselines (OneBit, co-authored) |

---

### Featured work

- **[QwenQuant](https://github.com/poojithdevan4D/QwenQuant)** — 4-way quantization benchmark (FP16 / INT8 / NF4 / Q4_K_M) on a 4 GB GPU. Caught a tokenizer measurement bug that made Q4_K_M look 75% worse than it was.
- **[qwen-speculative-decoding](https://github.com/poojithdevan4D/qwen-speculative-decoding)** — speculative decoding from scratch (Leviathan et al.), Qwen2.5-1.5B + 0.5B together on one 4 GB GPU, verified byte-for-byte against greedy.
- **[QuantEdge](https://github.com/poojithdevan4D/QuantEdge)** — INT8 inference on old ARM phones: hand-written NEON SIMD kernels (2.5× on a Cortex-A9) and TinyLlama on an Exynos 7870.
- **[superfloat](https://github.com/poojithdevan4D/superfloat)** · **[enterprise-llm-evaluator](https://github.com/poojithdevan4D/enterprise-llm-evaluator)**

---

### Stack

`Python` · `C / C++` · `CUDA C` · `PyTorch` · `llama.cpp / ggml` · `bitsandbytes` · `optimum-quanto`
`ARM NEON intrinsics` · `ONNX` · `TensorFlow Lite` · `Nsight` · familiar with `vLLM` / `TensorRT-LLM` / `CUDA Graphs`

**Quantization:** 1.58-bit ternary · Q1.15 fixed-point · INT4 NF4 · INT8 · Q4_K_M K-quants · KV-cache quantization

---

📫 **poojithdevan@gmail.com** · [LinkedIn](https://linkedin.com/in/poojith-devan)
