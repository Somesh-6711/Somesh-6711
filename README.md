<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./light.svg">
  <img alt="Somesh Panchal — Machine Learning Engineer" src="./dark.svg" width="100%">
</picture>

## Hey, I'm Somesh

I'm a Machine Learning Engineer in Dallas working on the serving side of LLMs — quantization, KV-cache reuse, batching, and the profiling work that tells you which of those actually helped. I care about the boring numbers: p99 latency, tokens per second, peak GPU memory, cost per request.

Most of my public work is benchmarking rather than modeling. I'd rather publish a reproducible comparison of six inference configurations than another fine-tuning notebook.

### Now building

A **reproducible benchmark suite** for LLM inference — same model, same workload, six serving configurations, measured end to end. The goal is that someone deciding between vLLM and ONNX Runtime for a small model can look at real numbers instead of vendor claims.

Alongside it, a **multi-agent SQL analyst** that turns plain-English questions into validated SQL, catches its own execution errors, and retries — evaluated against a single-shot baseline so the self-correction claim is testable rather than asserted.

### Projects

| Project | Result | What it is |
| :-- | :-- | :-- |
| [LLM Inference Benchmark Suite](https://github.com/Somesh-6711/LLM-Inference-Optimization-Benchmark-Suite) | ~3× throughput, ~60% less GPU memory vs. PyTorch baseline | Six configs on Qwen2.5-1.5B-Instruct — vanilla PyTorch, `torch.compile`, ONNX Runtime, GPTQ 4-bit, AWQ 4-bit, vLLM. Measures p50/p95/p99, tokens/sec, peak memory, and output quality on a held-out set. |
| [Multi-Agent SQL Analyst](https://github.com/Somesh-6711/Multi-Agent-SQL-Analyst) | Measured against a single-shot baseline on a Spider subset | Four LangGraph agents — planner, executor, critic, reporter. Read-only DB access, query allowlists, timeouts. FastAPI + Streamlit, containerized. |

<details>
<summary><b>How the benchmark suite is set up</b></summary>

<br>

Matched workloads across all six configurations, so the comparison isn't confounded by prompt length or batch shape. Quality is checked on a held-out evaluation set rather than assumed — a 4-bit config that gets fast by getting worse should show up as worse.

Profiling with PyTorch Profiler and `nvidia-smi` to find where time actually goes. The winning configuration ships behind a FastAPI service with streaming and request batching, packaged with Docker Compose, with GitHub Actions running lint, tests, and build.

A Grafana dashboard tracks latency, throughput, and GPU utilization over time. Methodology is documented so the numbers can be re-run rather than taken on faith.

</details>

### Stack

| Area | Tools |
| :-- | :-- |
| Inference | vLLM, GPTQ, AWQ, bitsandbytes, `torch.compile`, ONNX Runtime, TensorRT, KV cache, Flash Attention |
| Training | PyTorch DDP, FSDP, DeepSpeed ZeRO, mixed precision, gradient checkpointing |
| Serving | FastAPI, Triton Inference Server, TorchServe, request batching, streaming |
| Agents | LangGraph, LangChain, RAG, FAISS, pgvector, tool use |
| Data | PostgreSQL, SQL Server, Parquet, Pandas, NumPy |
| Infra | Docker, GitHub Actions, MLflow, Prometheus, Grafana, CUDA, Linux, AWS |
| Languages | Python, C++, SQL, Bash |

###  non-work thing

<img src="./leyendo-el-diario-periodico.gif" alt="freetime" width="200" align="left">&nbsp;&nbsp;&nbsp;

Football has been my thing since college — I played right wing forward through my bachelor's and still get out on the pitch when I can. The rest of my free time goes to games (shooters and soulslikes — Counter-Strike, Sekiro) and books, usually Indian history.

<br clear="left">

### Elsewhere

- Email — [someshpanchal11@gmail.com](mailto:someshpanchal11@gmail.com)
- LinkedIn — [linkedin.com/in/YOUR-HANDLE](https://www.linkedin.com/in/somesh-p-panchal)
- Based in Dallas, TX. Open to Machine Learning Engineer roles. 

---

Currently building a PC so my benchmarks stop being limited by the machine running them, and expanding the multi-agent SQL analyst.
