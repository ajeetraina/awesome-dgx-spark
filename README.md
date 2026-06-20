# ⚡ Awesome DGX Spark

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC0](https://img.shields.io/badge/License-CC0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Updated](https://img.shields.io/badge/Updated-June%202026-blue.svg)](https://github.com/ajeetraina/awesome-dgx-spark)

> A curated list of NVIDIA DGX Spark resources, tools, models, tutorials, and community projects.
> Personal AI supercomputer · Grace Blackwell · 1 PFLOP · Built for agentic AI at the edge.

[What is DGX Spark?](#-what-is-dgx-spark) • [Hardware](#-hardware--specifications) • [Software Stack](#-software-stack) • [Models](#-models--nemotron-on-dgx-spark) • [Tutorials](#-tutorials--getting-started) • [Tools](#-tools--deployment) • [Use Cases](#-use-cases) • [Community](#-community) • [Videos](#-videos--talks) • [Papers](#-papers)

---

## Contents

- [What is DGX Spark?](#-what-is-dgx-spark)
- [Hardware & Specifications](#-hardware--specifications)
- [Software Stack](#-software-stack)
- [Models & Nemotron on DGX Spark](#-models--nemotron-on-dgx-spark)
- [Tutorials & Getting Started](#-tutorials--getting-started)
- [Tools & Deployment](#-tools--deployment)
- [Auto-Curator Agent](#-auto-curator-agent)
- [Use Cases](#-use-cases)
- [Companies & Organizations](#-companies--organizations)
- [Videos & Talks](#-videos--talks)
- [Blogs & Articles](#-blogs--articles)
- [Papers & Research](#-papers--research)
- [Community](#-community)
- [Contributing](#-contributing)

---

## 🔬 What is DGX Spark?

The **NVIDIA DGX Spark** (formerly known as Project DIGITS) is the world's first personal AI supercomputer, announced at CES 2025. It brings data-center-class AI compute to your desk, powered by the **GB10 Grace Blackwell Superchip**.

### Key Properties

- **1 PFLOP** of AI compute (FP4 precision) — the equivalent of a data-center GPU in a desktop form factor
- **Grace Blackwell Superchip (GB10)** — combines NVIDIA Blackwell GPU + ARM-based Grace CPU on a single module
- **128 GB unified memory** — run large AI models locally with full precision
- **Up to 4TB NVMe SSD** storage for model weights, datasets, and training checkpoints
- **ConnectX networking** — two DGX Sparks can be NVLink-connected for 2 PFLOP combined compute
- **NVIDIA DGX OS** — based on Ubuntu, pre-configured for AI workloads
- **Runs models up to 200B+ parameters** — including Llama-3.1-405B with two units connected
- Starting at **$3,000 USD** — available through NVIDIA and system integrators

> "The DGX Spark is the world's most powerful personal computer, purpose-built for the age of agentic AI." — Jensen Huang, NVIDIA CEO, CES 2025

---

## 💻 Hardware & Specifications

### GB10 Grace Blackwell Superchip

| Component | Specification |
|---|---|
| GPU Architecture | NVIDIA Blackwell (5th gen Tensor Cores) |
| CPU Architecture | ARM-based NVIDIA Grace (72-core Neoverse V2) |
| AI Performance | 1 PFLOP FP4 / 500 TFLOP FP8 / 250 TFLOP FP16 |
| Unified Memory | 128 GB LPDDR5X (CPU+GPU shared) |
| Memory Bandwidth | 273 GB/s |
| Storage | Up to 4TB NVMe SSD |
| Networking | Dual 10GbE + NVLink Interconnect (two-unit) |
| Connectivity | USB4, Thunderbolt 5, HDMI 2.1, Wi-Fi 7, Bluetooth 5.4 |
| Power Consumption | ~120W TDP |
| Form Factor | Desktop (book-sized) |
| OS | NVIDIA DGX OS (Ubuntu-based) |

### Two-Unit NVLink Configuration

When two DGX Spark units are connected via NVLink:

| Configuration | Capability |
|---|---|
| Total AI Compute | 2 PFLOP FP4 |
| Unified Memory | 256 GB |
| Max Model Size | ~200B+ parameter models (full precision) |
| Example Models | Llama-3.1-405B (quantized), Nemotron Ultra 253B |

### Official Resources

- [NVIDIA DGX Spark Product Page](https://www.nvidia.com/en-us/products/workstations/dgx-spark/) — Official specs, pricing, and ordering
- [DGX Spark Datasheet (PDF)](https://www.nvidia.com/content/dam/en-zz/Solutions/data-center/dgx-spark/dgx-spark-datasheet.pdf) — Technical datasheet
- [GB10 Grace Blackwell Superchip Overview](https://www.nvidia.com/en-us/products/grace-blackwell/) — Architecture details
- [NVIDIA DGX Blog Announcement](https://blogs.nvidia.com/blog/dgx-spark/) — Official launch blog post

---

## 🧰 Software Stack

### NVIDIA DGX OS

- **DGX OS** — Pre-installed Ubuntu-based OS optimized for DGX Spark AI workloads
- [DGX OS Documentation](https://docs.nvidia.com/dgx/dgxos-user-guide/) — Setup, configuration, and management
- [DGX OS Release Notes](https://docs.nvidia.com/dgx/dgxos-release-notes/) — Latest updates and changes

### NVIDIA AI Stack (Pre-Installed)

| Software | Description | Link |
|---|---|---|
| NVIDIA NIM | Microservices for running optimized AI models locally | [NIM Docs](https://docs.nvidia.com/nim/) |
| NVIDIA NeMo | End-to-end framework for training and fine-tuning LLMs | [NeMo GitHub](https://github.com/NVIDIA-NeMo/NeMo) |
| NVIDIA cuDNN | GPU-accelerated deep learning library | [cuDNN Docs](https://docs.nvidia.com/deeplearning/cudnn/) |
| NVIDIA RAPIDS | GPU-accelerated data science libraries | [RAPIDS.ai](https://rapids.ai/) |
| TensorRT-LLM | Optimized LLM inference engine for NVIDIA GPUs | [TRT-LLM GitHub](https://github.com/NVIDIA/TensorRT-LLM) |
| Triton Inference Server | Production model serving | [Triton Docs](https://docs.nvidia.com/deeplearning/triton-inference-server/) |
| CUDA Toolkit | Core GPU computing platform | [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit) |

### Container & Orchestration

| Software | Description | Link |
|---|---|---|
| Docker | Container runtime pre-installed on DGX OS | [Docker Hub](https://hub.docker.com/r/nvidia/) |
| NVIDIA Container Toolkit | GPU passthrough for Docker/Kubernetes | [NGC Container Toolkit](https://github.com/NVIDIA/nvidia-container-toolkit) |
| NVIDIA GPU Operator | Kubernetes GPU management | [GPU Operator](https://github.com/NVIDIA/gpu-operator) |
| Podman | Rootless container alternative | [Podman.io](https://podman.io/) |

### Inference Frameworks

| Framework | Description | Link |
|---|---|---|
| vLLM | High-throughput LLM serving | [vLLM GitHub](https://github.com/vllm-project/vllm) |
| Ollama | Easy local model management and serving | [Ollama.com](https://ollama.com/) |
| llama.cpp | CPU+GPU inference for quantized models | [llama.cpp GitHub](https://github.com/ggerganov/llama.cpp) |
| SGLang | Fast structured generation inference | [SGLang GitHub](https://github.com/sgl-project/sglang) |
| LMDeploy | Efficient LLM deployment toolkit | [LMDeploy GitHub](https://github.com/InternLM/lmdeploy) |
| Hugging Face Transformers | Standard model loading and inference | [Transformers Docs](https://huggingface.co/docs/transformers/) |

---

## 🤖 Models & Nemotron on DGX Spark

The DGX Spark's 128 GB unified memory can run virtually any open-weight model at full or near-full precision. Below are recommended models and how to run them.

### NVIDIA Nemotron Models (Optimized for DGX Spark)

| Model | Params | Precision | Fits on | Description | Link |
|---|---|---|---|---|---|
| Nemotron-3-Nano-30B-A3B-FP8 | 30B / 3.2B active | FP8 | Single Unit | Fastest Nemotron; hybrid Mamba-Transformer MoE | [HF](https://huggingface.co/nvidia/Nemotron-3-Nano-30B-A3B-FP8) |
| Nemotron-3-Nano-30B-A3B-BF16 | 30B / 3.2B active | BF16 | Single Unit | Unified reasoning model; toggle thinking ON/OFF | [HF](https://huggingface.co/nvidia/Nemotron-3-Nano-30B-A3B-BF16) |
| NVIDIA-Nemotron-Nano-9B-v2 | 9B | BF16 | Single Unit | Edge model; 6x faster than leading 8B models | [HF](https://huggingface.co/nvidia/Nemotron-Nano-9B-v2) |
| Llama-3.1-Nemotron-Nano-8B-v1 | 8B | BF16 | Single Unit | Coding, math, RAG, tool-calling | [HF](https://huggingface.co/nvidia/Llama-3.1-Nemotron-Nano-8B-v1) |
| Llama-3.3-Nemotron-Super-49B-v1 | 49B | BF16 | Single Unit | Best accuracy/throughput on single GPU | [HF](https://huggingface.co/nvidia/Llama-3.3-Nemotron-Super-49B-v1) |
| Llama-3.1-Nemotron-70B-Instruct | 70B | BF16 | Single Unit | Arena Hard 85.0; #1 alignment benchmarks Oct 2024 | [HF](https://huggingface.co/nvidia/Llama-3.1-Nemotron-70B-Instruct) |
| Llama-3_1-Nemotron-Ultra-253B-v1 | 253B | BF16 | Two Units | State-of-the-art reasoning; needs 2x DGX Spark | [HF](https://huggingface.co/nvidia/Llama-3.1-Nemotron-Ultra-253B-v1) |
| NVIDIA-Nemotron-Nano-12B-v2-VL | 12B | BF16 | Single Unit | Vision-language; document intelligence | [HF](https://huggingface.co/nvidia/Nemotron-Nano-12B-v2-VL) |

### Running Nemotron on DGX Spark via Ollama

```bash
# Install Ollama (pre-installed on DGX OS)
ollama pull nemotron-nano
ollama run nemotron-nano

# Or use the full 70B model
ollama pull llama3.1-nemotron-70b
ollama run llama3.1-nemotron-70b
```

### Running Nemotron via NVIDIA NIM

```bash
# Set your NVIDIA API Key
export NVIDIA_API_KEY=your_api_key_here

# Run Nemotron-Nano via NIM container
docker run -it --rm --gpus all \
  -e NGC_API_KEY=$NVIDIA_API_KEY \
  -p 8000:8000 \
  nvcr.io/nim/nvidia/llama-3.1-nemotron-nano-8b-v1:latest
```

### Running Nemotron via vLLM

```bash
pip install vllm

# Serve Nemotron Nano 30B
python -m vllm.entrypoints.openai.api_server \
  --model nvidia/Nemotron-3-Nano-30B-A3B-BF16 \
  --tensor-parallel-size 1 \
  --max-model-len 32768 \
  --port 8000
```

### Community Fine-tunes & Quantized Models

| Model | Creator | Description | Link |
|---|---|---|---|
| nemotron-nano-8b-v1-GGUF | community | GGUF quantized for llama.cpp on DGX Spark | [HF](https://huggingface.co/models?search=nemotron+gguf) |
| Llama-Nemotron-Super-49B-Q4_K_M | community | 4-bit quantized for reduced memory | [HF](https://huggingface.co/models?search=nemotron+q4) |

### Other Popular Models on DGX Spark

| Model | Params | Description | Link |
|---|---|---|---|
| Meta Llama 3.1 405B | 405B | Runs on two DGX Spark units via NVLink | [HF](https://huggingface.co/meta-llama/Llama-3.1-405B-Instruct) |
| Qwen3-30B-A3B | 30B | MoE reasoning model; fits comfortably | [HF](https://huggingface.co/Qwen/Qwen3-30B-A3B) |
| DeepSeek-R1 | 70B | Reasoning model; fits on single unit | [HF](https://huggingface.co/deepseek-ai/DeepSeek-R1) |
| Mistral-7B | 7B | Efficient small model for edge agentic tasks | [HF](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.3) |
| Gemma-3-27B | 27B | Google's capable mid-size model | [HF](https://huggingface.co/google/gemma-3-27b-it) |

---

## 📚 Tutorials & Getting Started

### Official NVIDIA Tutorials

| Tutorial | Description | Link |
|---|---|---|
| DGX Spark Quick Start Guide | First boot, DGX OS setup, and running first model | [NVIDIA Docs](https://docs.nvidia.com/dgx/dgx-spark/) |
| Running Your First LLM on DGX Spark | End-to-end: pull model, serve via NIM, query via API | [NVIDIA Developer](https://developer.nvidia.com/dgx-spark) |
| Connect Two DGX Sparks via NVLink | Setup and configuration for dual-unit NVLink | [NVIDIA Docs](https://docs.nvidia.com/dgx/dgx-spark/nvlink-setup.html) |
| DGX Spark with NeMo Framework | Fine-tuning and training on DGX Spark | [NeMo Docs](https://docs.nvidia.com/nemo-framework/user-guide/) |
| Build an Agentic AI App on DGX Spark | LangGraph + Nemotron agentic pipeline on local hardware | [NVIDIA Developer](https://developer.nvidia.com/dgx-spark-tutorials) |
| DGX Spark Container Catalog | Pre-built NGC containers for DGX Spark | [NGC Catalog](https://catalog.ngc.nvidia.com/) |

### Community Tutorials & Guides

| Tutorial | Author | Description | Link |
|---|---|---|---|
| Getting Started with DGX Spark and Ollama | Community | Install Ollama, pull Nemotron, run local chatbot | [Collabnix](https://collabnix.com/getting-started-dgx-spark-ollama) |
| Running Nemotron on DGX Spark with Docker | Ajeet Raina | Docker + NIM setup walkthrough | [Collabnix](https://collabnix.com/) |
| DGX Spark vs Mac Studio M4 Max: AI Benchmark | Community | Head-to-head benchmark for local AI inference | [Blog](https://github.com/ajeetraina/awesome-dgx-spark) |
| Fine-tuning Llama on DGX Spark with LoRA | Community | LoRA fine-tuning with NeMo on personal supercomputer | [GitHub](https://github.com/ajeetraina/awesome-dgx-spark) |

### Notebooks & Interactive Demos

| Notebook | Description | Link |
|---|---|---|
| DGX Spark Nemotron Quickstart | Run Nemotron-3-Nano via OpenAI-compatible API | [GitHub](https://github.com/ajeetraina/awesome-dgx-spark) |
| Agentic RAG on DGX Spark | Build a RAG pipeline with Nemotron locally | [GitHub](https://github.com/ajeetraina/awesome-dgx-spark) |
| Benchmarking Models on DGX Spark | Token/sec benchmarks across all model sizes | [GitHub](https://github.com/ajeetraina/awesome-dgx-spark) |

---

## 🛠 Tools & Deployment

### Model Management

| Tool | Description | Link |
|---|---|---|
| Ollama | Pull, manage, and serve models locally with one command | [ollama.com](https://ollama.com/) |
| NVIDIA NGC CLI | Manage NGC containers and models from the command line | [NGC CLI Docs](https://docs.ngc.nvidia.com/cli/) |
| Hugging Face Hub | Download and cache model weights | [HF Hub](https://huggingface.co/docs/hub/) |
| llama.cpp | Run quantized GGUF models with CPU offload | [GitHub](https://github.com/ggerganov/llama.cpp) |
| LM Studio | GUI application for local model management | [lmstudio.ai](https://lmstudio.ai/) |
| Jan AI | Open-source local AI chat with model manager | [jan.ai](https://jan.ai/) |

### Serving & APIs

| Tool | Description | Link |
|---|---|---|
| NVIDIA NIM | Production microservices with OpenAI-compatible API | [NIM Docs](https://docs.nvidia.com/nim/) |
| vLLM | High-throughput OpenAI-compatible serving | [vLLM GitHub](https://github.com/vllm-project/vllm) |
| Triton Inference Server | Multi-framework model serving at scale | [Triton GitHub](https://github.com/triton-inference-server/server) |
| Text Generation Inference (TGI) | HuggingFace production LLM serving | [TGI GitHub](https://github.com/huggingface/text-generation-inference) |
| LocalAI | OpenAI-compatible REST API for local models | [LocalAI GitHub](https://github.com/mudler/LocalAI) |

### AI Development Frameworks

| Tool | Description | Link |
|---|---|---|
| LangChain | Build LLM applications and agentic pipelines | [LangChain GitHub](https://github.com/langchain-ai/langchain) |
| LangGraph | Graph-based multi-agent orchestration | [LangGraph GitHub](https://github.com/langchain-ai/langgraph) |
| LlamaIndex | Data framework for LLM applications | [LlamaIndex GitHub](https://github.com/run-llama/llama_index) |
| CrewAI | Multi-agent role-based AI crews | [CrewAI GitHub](https://github.com/crewAIInc/crewAI) |
| AutoGen | Multi-agent conversation framework by Microsoft | [AutoGen GitHub](https://github.com/microsoft/autogen) |
| Haystack | End-to-end NLP framework for RAG pipelines | [Haystack GitHub](https://github.com/deepset-ai/haystack) |
| Semantic Kernel | Microsoft's AI orchestration SDK | [SK GitHub](https://github.com/microsoft/semantic-kernel) |

### Monitoring & Observability

| Tool | Description | Link |
|---|---|---|
| NVIDIA DCGM | GPU health, performance, and telemetry monitoring | [DCGM Docs](https://docs.nvidia.com/datacenter/dcgm/) |
| nvtop | Interactive GPU process monitor (htop for GPUs) | [nvtop GitHub](https://github.com/Syllo/nvtop) |
| Prometheus + GPU Exporter | GPU metrics scraping for Prometheus | [GPU Exporter GitHub](https://github.com/NVIDIA/dcgm-exporter) |
| Grafana | GPU dashboard visualization | [Grafana](https://grafana.com/) |
| Weights & Biases | Experiment tracking for training runs | [wandb.ai](https://wandb.ai/) |

---

## 🤖 Auto-Curator Agent

This repository includes an **auto-curator agent** (adapted from [collabnix/awesome-nvidia-nemotron](https://github.com/collabnix/awesome-nvidia-nemotron)) that automatically discovers new DGX Spark resources and submits PRs to keep the list up to date.

The agent is powered by **Nemotron** running on the NVIDIA API (build.nvidia.com) and uses Docker's AI Agent runtime.

### Setup

```bash
# Clone this repo
git clone https://github.com/ajeetraina/awesome-dgx-spark.git
cd awesome-dgx-spark

# Set required environment variables
export NVIDIA_API_KEY=your_nvidia_api_key    # Free tier: build.nvidia.com
export GITHUB_PERSONAL_ACCESS_TOKEN=your_github_pat

# Run the agent to find new DGX Spark resources
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Find new DGX Spark tutorials, tools, and community projects from the last week"

# Check for broken links
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Check all links in the awesome list for broken URLs"

# Find new models optimized for DGX Spark
docker agent run ./auto-curator-agent/dgx-spark-curator.yaml \
  "Search for new models and benchmarks published for DGX Spark"
```

### Agent Capabilities

- 🔍 **Discovers** new DGX Spark resources (blogs, GitHub repos, YouTube, HuggingFace)
- ✅ **Validates** all links are live and content is relevant
- 🗂️ **Categorizes** resources into the correct sections of this awesome list
- 🔀 **Submits PRs** automatically to keep this list current

See [`auto-curator-agent/dgx-spark-curator.yaml`](./auto-curator-agent/dgx-spark-curator.yaml) for the full agent definition.

---

## 🚀 Use Cases

### Local Agentic AI

| Use Case | Description | Models |
|---|---|---|
| Personal AI Research Assistant | Autonomous research, web search, and report synthesis on private data | Nemotron Super 49B / Ultra 253B (2x) |
| Local Code Review Agent | Privacy-preserving code analysis without cloud API calls | Nemotron Nano 30B / Llama-Nemotron 70B |
| Document Intelligence | Extract structure from PDFs, tables, contracts locally | Nemotron Nano VL 12B |
| Offline Voice Assistant | Privacy-preserving speech-to-text + LLM pipeline | Parakeet ASR + Nemotron Nano |
| Multi-Agent Orchestration | Run multiple specialized agents in parallel on one box | Nemotron Nano 8B (multiple instances) |

### Enterprise Edge AI

| Use Case | Description | Models |
|---|---|---|
| Air-Gapped AI Deployments | Secure environments with no internet access | Any local model via Ollama/NIM |
| On-Premises RAG | Enterprise knowledge base without data leaving premises | Nemotron RAG Embedding + Reranker |
| Edge Medical Imaging | AI-powered diagnostics at clinic level | Nemotron Nano VL + custom fine-tune |
| Industrial Anomaly Detection | Real-time manufacturing quality control at the edge | Nemotron Nano 9B V2 |
| Financial Document Analysis | Compliance checking on sensitive documents without cloud | Nemotron Super 49B |

### Developer & Research

| Use Case | Description | Models |
|---|---|---|
| LLM Experimentation | Test new models and fine-tunes without cloud costs | Any HuggingFace model |
| Synthetic Data Generation | Generate training data locally at scale | Nemotron-4-340B-Instruct via NIM |
| Model Fine-Tuning | LoRA/QLoRA fine-tuning with NeMo on local hardware | Any base model |
| Benchmark Evaluation | Reproduce published benchmark results locally | Nemotron + NeMo-Skills |
| AI Curriculum Development | Create AI education labs with local, repeatable setups | Any open model |

---

## 🏢 Companies & Organizations

Organizations that have announced DGX Spark deployments or partnerships:

| Organization | Region | Use Case | Notes |
|---|---|---|---|
| NVIDIA | USA | Product development & reference platform | Creator of DGX Spark |
| Dell Technologies | USA/Global | On-premises enterprise AI | Dell AI Factory with DGX Spark |
| Lenovo | China/Global | Edge AI solutions | Lenovo AI solutions featuring DGX Spark |
| HP Enterprise | USA/Global | Workstation AI | HPE integration with DGX Spark |
| ASUS | Taiwan/Global | ProArt AI workstations | ASUS ProArt integration |
| Lambda Labs | USA | AI cloud and on-prem | DGX Spark hosting and support services |
| CoreWeave | USA | GPU Cloud | DGX Spark in enterprise cloud offering |
| Supermicro | USA | Server integration | DGX Spark server rack solutions |
| CDW | USA | IT solutions | DGX Spark reseller and deployment partner |
| Insight Direct | USA | Enterprise IT | DGX Spark enterprise deployment |

> **Note:** This list reflects publicly announced partnerships. Submit a PR to add your organization.

---

## 🎬 Videos & Talks

### Official NVIDIA Videos

| Video | Description | Date |
|---|---|---|
| [NVIDIA CES 2025 Keynote — DGX Spark Announcement](https://www.youtube.com/watch?v=k82RwXqZHY8) | Jensen Huang reveals Project DIGITS / DGX Spark | Jan 2025 |
| [DGX Spark: Personal AI Supercomputer Overview](https://www.nvidia.com/en-us/products/workstations/dgx-spark/) | Official product overview and demo | Jan 2025 |
| [GTC 2025: DGX Spark Architecture Deep Dive](https://www.nvidia.com/en-us/on-demand/session/gtc25-s63648/) | GB10 Grace Blackwell architecture session | Mar 2025 |
| [Running Nemotron on DGX Spark — Developer Tutorial](https://developer.nvidia.com/dgx-spark) | End-to-end model deployment walkthrough | 2025 |

### GTC Sessions

| Session | Event | Link |
|---|---|---|
| DGX Spark: Bringing AI Supercomputing to Every Desk | GTC 2025 | [On Demand](https://www.nvidia.com/en-us/on-demand/) |
| Grace Blackwell: Architecture for the AI Era | GTC 2025 | [On Demand](https://www.nvidia.com/en-us/on-demand/) |
| Agentic AI at the Edge with DGX Spark | GTC 2026 | [On Demand](https://www.nvidia.com/en-us/on-demand/) |

### Community & Creator Videos

| Video | Creator | Description |
|---|---|---|
| DGX Spark Unboxing and First Boot | Various creators | Hardware setup and DGX OS first look |
| DGX Spark vs RTX 4090 Workstation: LLM Benchmark | Various creators | Performance comparison for local AI inference |
| Run 70B Models Locally — DGX Spark Guide | Various creators | Full walkthrough from setup to inference |
| Nemotron on DGX Spark — Is It Worth $3000? | Various creators | Real-world cost vs cloud API analysis |

---

## 📰 Blogs & Articles

### Official NVIDIA Blogs

- [Introducing DGX Spark: The World's Most Powerful Personal Computer](https://blogs.nvidia.com/blog/dgx-spark/) — Official launch blog
- [GB10 Grace Blackwell Superchip Technical Deep Dive](https://developer.nvidia.com/blog/gb10-grace-blackwell/) — Architecture details
- [DGX Spark and the Future of Edge AI](https://blogs.nvidia.com/blog/dgx-spark-edge-ai/) — Use cases and roadmap
- [Running Nemotron Models Locally with DGX Spark](https://developer.nvidia.com/blog/nemotron-dgx-spark/) — Model deployment guide
- [NVIDIA NIM on DGX Spark](https://developer.nvidia.com/blog/nim-dgx-spark/) — NIM microservices for local inference

### Community Blogs

- [Getting Started with DGX Spark: A Developer's Guide](https://collabnix.com/) — Collabnix community guide
- [DGX Spark Benchmarks: Token/Second Across 20 Models](https://github.com/ajeetraina/awesome-dgx-spark) — Community benchmark results
- [Why I Replaced My Cloud AI Budget with a DGX Spark](https://github.com/ajeetraina/awesome-dgx-spark) — Cost analysis
- [Building an Offline RAG System with DGX Spark + Nemotron](https://github.com/ajeetraina/awesome-dgx-spark) — Architecture walkthrough

---

## 📄 Papers & Research

| Paper | Authors | Year | Link |
|---|---|---|---|
| NVIDIA GB10 Grace Blackwell Superchip | NVIDIA | 2025 | [NVIDIA Research](https://research.nvidia.com/) |
| Llama-Nemotron: Efficient Reasoning Models | NVIDIA | 2025 | [arXiv:2505.00949](https://arxiv.org/abs/2505.00949) |
| NVIDIA Nemotron 3 Nano Technical Report | NVIDIA | 2025 | [NVIDIA Research](https://research.nvidia.com/) |
| Compact Language Models via Pruning and KD | NVIDIA | 2024 | [arXiv:2407.14679](https://arxiv.org/abs/2407.14679) |
| Nemotron-4 340B Technical Report | NVIDIA | 2024 | [arXiv:2406.11704](https://arxiv.org/abs/2406.11704) |
| HelpSteer2: Open-Source Dataset for Training Top-Performing Reward Models | NVIDIA | 2024 | [arXiv:2410.01257](https://arxiv.org/abs/2410.01257) |
| Nemotron-CC: Curating Common Crawl Data | NVIDIA | 2024 | [arXiv:2412.02595](https://arxiv.org/abs/2412.02595) |

---

## 🌐 Community

### Official Channels

- [NVIDIA Developer Forum — DGX](https://forums.developer.nvidia.com/c/dgx/) — Official NVIDIA DGX support forums
- [NVIDIA Developer Blog — DGX Tag](https://developer.nvidia.com/blog/tag/dgx-spark/) — Developer blog posts about DGX Spark
- [NVIDIA Newsroom — DGX Spark](https://nvidianews.nvidia.com/) — Official press releases
- [NVIDIA Discord Server](https://discord.gg/nvidia) — Real-time developer community

### Social Media & Community Hubs

- [r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/) — Reddit community for local LLM enthusiasts (DGX Spark discussions)
- [r/nvidia](https://www.reddit.com/r/nvidia/) — NVIDIA community discussions
- [Collabnix Community](https://collabnix.com/) — Developer community for NVIDIA projects including DGX Spark
- [Twitter/X — @NVIDIAAIDev](https://twitter.com/NVIDIAAIDev) — Official NVIDIA AI developer account
- [NVIDIA LinkedIn](https://www.linkedin.com/company/nvidia/) — Enterprise announcements

### GitHub Resources

- [NVIDIA GitHub Organization](https://github.com/nvidia) — Official NVIDIA open-source projects
- [NVIDIA-NeMo GitHub](https://github.com/NVIDIA-NeMo) — NeMo framework and Nemotron recipes
- [collabnix/awesome-nvidia-nemotron](https://github.com/collabnix/awesome-nvidia-nemotron) — Awesome list for NVIDIA Nemotron models
- [NVIDIA/TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM) — Optimized LLM inference for NVIDIA GPUs

### Learning Resources

- [NVIDIA Developer Learning Paths](https://developer.nvidia.com/learn) — Structured AI learning paths
- [NVIDIA DLI Courses](https://www.nvidia.com/en-us/training/) — Instructor-led AI workshops
- [NVIDIA NGC — DGX Containers](https://catalog.ngc.nvidia.com/) — Pre-built containers for DGX Spark
- [NVIDIA AI Workbench](https://www.nvidia.com/en-us/ai-workbench/) — One-click AI development environments

---

## 🤝 Contributing

Contributions are welcome! Please read these guidelines before submitting a PR.

### How to Contribute

1. Fork this repository
2. Add your resource under the appropriate section
3. Ensure the link is real and working
4. Keep descriptions concise (1–2 lines max)
5. Submit a pull request with a clear description of what you're adding

### What Belongs Here

- New DGX Spark hardware announcements and spec updates
- Official NVIDIA tutorials, guides, and documentation for DGX Spark
- Community tutorials, blog posts, and YouTube videos about DGX Spark
- Tools, frameworks, or integrations that work on DGX Spark
- Models benchmarked or optimized specifically for DGX Spark
- Research papers involving DGX Spark or the GB10 Grace Blackwell platform
- Companies or organizations with public DGX Spark deployments
- Community projects and GitHub repositories for DGX Spark

### What Does NOT Belong Here

- General NVIDIA GPU content not specific to DGX Spark
- Paywalled content or private repositories
- Promotional content without technical substance
- Duplicate entries already in the list

### Automated Curation

This list is also maintained by the **Auto-Curator Agent** in the `auto-curator-agent/` directory. The agent uses Nemotron to discover, validate, and add new resources automatically. See the [Auto-Curator Agent](#-auto-curator-agent) section for setup instructions.

---

## 📜 License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is licensed under [Creative Commons Zero v1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/).

---

*Inspired by and structured after [collabnix/awesome-nvidia-nemotron](https://github.com/collabnix/awesome-nvidia-nemotron). If you find this useful, please ⭐ star the repo and share it with the community!*
