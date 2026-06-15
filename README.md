<p align="center">
  <img src="https://user-images.githubusercontent.com/61057666/169029838-74df663d-2e62-4d77-bdff-b43f7d63f00f.png" width="100%" />
</p>
<h1 align="center">Nikhil Mourya</h1>
<p align="center"><b>ML Engineer · Multi-Agent Systems · Production NLP</b></p>
<p align="center"><i>I build systems that know when they don't know enough, then loop until they do.</i></p>

---

I work at the intersection of LLM systems and production ML — multi-agent orchestration, efficient fine-tuning, and RAG pipelines that actually ship. My projects aren't independent experiments; they follow a single question: *how much complexity can you hide before the system stops being useful?*

---

Third year at BIT Mesra, studying what doesn't fit in a lecture hall.

---

Software Engineer — ML at [HireBuddy](https://www.hirebuddy.net) *(May–Nov 2025)* — built AI hiring infrastructure processing 10K+ resumes/day in production.

```
focus     : multi-agent systems · efficient LLMs · RAG pipelines · production ML
currently : open to ML internships & full-time opportunities
location  : Jaipur, India
cf        : Specialist 1400+
```

---

## What I Actually Build

| Project | The Question I Was Answering | Result |
|---|---|---|
| [HiveMind](https://github.com/TryingtobeingNikhil/HiveMind) | Can a research system know when its own answer isn't good enough — and fix it? | 5-agent pipeline, autonomous eval loop, deterministic confidence scoring |
| [CodeLens](https://github.com/TryingtobeingNikhil/CodeLens) | Can you search a codebase by intent, not keywords — fully offline? | VS Code extension, AST chunking, 9K+ chunks, sub-10ms search · [Demo ↗](https://youtu.be/d2I2omkHVLE) |
| [Pruned U-Net](https://github.com/TryingtobeingNikhil/Pruned-UNet-Biomedical-Segmentation) | How much of a segmentation model is actually load-bearing? | 97.3% params removed, IoU > 0.95 held · IIT Kharagpur |
| [PEGASUS + LoRA](https://github.com/TryingtobeingNikhil/pegasus-lora-efficient-summarization) | Can you fine-tune a 767M model on a student budget? | 99.8% param reduction, 27× faster training |
| [Vectorless RAGs](https://github.com/TryingtobeingNikhil/Vectorless-RAGs) | Is a vector database a requirement or just a habit? | Full retrieval pipeline, zero embeddings, zero vector DB |
| [AttentionIsALLICode](https://github.com/TryingtobeingNikhil/AttentionIsALLICode) | Do I actually understand attention, or just import it? | Full GPT-style LM, zero frameworks |

---

## Projects

### 🧠 HiveMind · Autonomous Deep Research System
*May 2026 · [GitHub](https://github.com/TryingtobeingNikhil/HiveMind)*

**The problem:** Standard RAG retrieves once and answers. There's no quality check, no critique, no "did I actually answer this?" — just one generation pass and a confident-sounding response.

**What I built:** A production-grade autonomous research system with a 5-agent sequential pipeline: Planner → Researcher → Critic → Writer → Evaluator. The orchestrator decomposes queries into tasks, retrieves evidence via ChromaDB + cosine reranking, critiques findings, writes a structured report, then evaluates whether confidence is sufficient. If not — it identifies gaps and loops, researching only the missing pieces.

**The key decision:** Confidence is calculated as the mean vector retrieval score, not self-reported by the LLM. LLMs hallucinate confidence. Math doesn't.

**Infra:** asyncio.Lock for single-threaded LLM execution (prevents OOM on local hardware + Groq rate-limit bursts) · Docker Compose (FastAPI + Redis task queue + ChromaDB + OpenTelemetry distributed tracing) · SSE streaming for real-time pipeline state

`Python` `FastAPI` `ChromaDB` `Redis` `OpenTelemetry` `Groq` `Ollama` `Docker` `Pydantic` `asyncio`

[→ View Repository](https://github.com/TryingtobeingNikhil/HiveMind)

---

### 🔍 CodeLens · Offline Semantic Code Search (VS Code Extension)
*Apr 2026 · [GitHub](https://github.com/TryingtobeingNikhil/CodeLens) · [Demo ↗](https://youtu.be/d2I2omkHVLE)*

**The problem:** You join a large codebase. You know there's *some* function that handles JWT token refresh — but `Ctrl+F "token"` returns 847 matches. Traditional search matches text, not intent.

**What I built:** A fully offline VS Code extension that indexes your codebase using AST-based chunking (tree-sitter) and 768-dim embeddings via Ollama. Natural language query → ranked semantic results → one-click jump to the exact line. No internet, no API keys, no cloud.

**Results:** 9K+ chunks indexed · sub-10ms ANN lookup · auto-reindexes on file save via MD5 hashing · optional Mistral 7B explain mode

`Python` `TypeScript` `FastAPI` `tree-sitter` `Ollama` `VS Code API` `Docker`

[→ View Repository](https://github.com/TryingtobeingNikhil/CodeLens) · [→ Watch Demo](https://youtu.be/d2I2omkHVLE)

---

### 🧬 Pruned U-Net · Biomedical Segmentation
*Mar 2025 · IIT Kharagpur research collaboration · [GitHub](https://github.com/TryingtobeingNikhil/Pruned-UNet-Biomedical-Segmentation)*

**The problem:** U-Net for biomedical segmentation is over-parameterized by design — built for generality, not efficiency. Most medical imaging deployments don't need that headroom.

**What I built:** Structured magnitude pruning pipeline targeting channels, not individual weights. The key finding: IoU degraded sharply after ~96% reduction but held flat before that — meaning there's a wide safe compression window most implementations never explore.

**Results:** 97.3% parameter reduction · 92% FLOPs reduction · IoU > 0.95 on MoNuSeg

`PyTorch` `U-Net` `Model Pruning` `Computer Vision` `MoNuSeg`

[→ View Repository](https://github.com/TryingtobeingNikhil/Pruned-UNet-Biomedical-Segmentation)

---

### 📝 PEGASUS + LoRA · Efficient Summarization
*Feb 2026 · [GitHub](https://github.com/TryingtobeingNikhil/pegasus-lora-efficient-summarization)*

**The problem:** Full fine-tuning a 767M parameter model requires compute most practitioners don't have.

**What I built:** LoRA rank-decomposition adapters via HuggingFace PEFT on BBC XSum, targeting attention weight matrices. Rank selection (r=16) was the critical decision — lower ranks trained faster but degraded ROUGE scores noticeably; higher ranks approached full fine-tuning cost. Full fine-tuning produced word salad on unseen domains. LoRA didn't.

**Results:** 767M → 1.57M trainable parameters (99.8% reduction) · 27× faster training (260s → 9.5s)

`PyTorch` `HuggingFace` `PEFT` `LoRA` `NLP` `XSum`

[→ View Repository](https://github.com/TryingtobeingNikhil/pegasus-lora-efficient-summarization)

---

### 🔍 Vectorless RAGs
*Ongoing · [GitHub](https://github.com/TryingtobeingNikhil/Vectorless-RAGs)*

**The problem:** Vector databases have become the default assumption in RAG architectures. I wanted to know if that default is load-bearing or just conventional.

**What I built:** Full RAG pipeline using LLM-guided tree traversal — no embeddings, no vector index, no similarity search. Performs well on structured, domain-specific corpora; degrades on semantically ambiguous queries where dense retrieval has a real advantage.

*Half the RAG stacks I see are a vector DB cosplaying as a product requirement.*

`Python` `Ollama` `LLaMA 3` `RAG` `Tree Traversal` `Streamlit`

[→ View Repository](https://github.com/TryingtobeingNikhil/Vectorless-RAGs)

---

### 🔤 AttentionIsALLICode · GPT Transformer from Scratch
*Oct 2025 · [GitHub](https://github.com/TryingtobeingNikhil/AttentionIsALLICode)*

**The problem:** Most people use transformers. Fewer understand what's actually happening inside the attention computation.

**What I built:** Full GPT-style character-level language model in raw PyTorch trained on Tiny Shakespeare — multi-head self-attention, causal masking, positional encoding, residual connections, layer norm, custom training loop with gradient clipping and cosine LR schedule.

`PyTorch` `Transformers` `NLP` `From Scratch`

[→ View Repository](https://github.com/TryingtobeingNikhil/AttentionIsALLICode)

---

## Production Experience

**Software Engineer — Machine Learning · [HireBuddy](https://www.hirebuddy.net)** *(May 2025 – Nov 2025)*

Built ML infrastructure from zero — India-specific resume scoring system via transformer embeddings and RAG pipelines, improving shortlist precision by 35% over keyword-matching baseline. Evaluation stack using RAGAS and LangSmith to measure retrieval quality and response grounding. FastAPI + Docker deployment on AWS serving 10K+ resumes/day through a REST API.

Key decisions: chunking strategy for resume parsing, reranking pipeline design, latency vs accuracy tradeoff for real-time scoring.

---

## Hackathons

**Smart India Hackathon 2024 · Finalist**
ML-based hospital queue prioritization — 28% predicted wait time reduction. The constraint that made it interesting: the model had to be explainable to non-technical hospital staff, not just accurate.

**IIIT Delhi Hackathon 2023 · Finalist**
ResNet50 classifier, 94% accuracy, 30% training time reduction via mixed-precision training. The win came from profiling the data loading bottleneck, not the model itself.

---

## Skills

**Core:** Python · C++ · PyTorch · TensorFlow · HuggingFace · Scikit-learn  
**LLMs & RAG:** LangChain · LangGraph · PEFT · LoRA · Transformers · RAG Pipelines · OpenAI API · Groq API · Ollama  
**Eval & Observability:** RAGAS · LangSmith · OpenTelemetry · offline eval pipelines  
**Deployment:** FastAPI · Docker · AWS · Redis · ChromaDB · FAISS · REST APIs · asyncio · Pydantic  
**Data:** NumPy · Pandas · Matplotlib · SQL  
**CP:** Codeforces Specialist (1400+)  

---

## Achievements
- 🥇 Finalist — Smart India Hackathon 2024
- 🥇 Finalist — IIIT Delhi Hackathon 2023
- 💻 Codeforces Specialist — 1400+
- 🎯 200+ problems solved across CP platforms

---

## Connect

<p align="center">
  <a href="mailto:tsmftxnikhil14@gmail.com">
    <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>
  <a href="https://www.linkedin.com/in/nikhil-mourya-36913a300/">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
  <a href="https://tryingtobenikhil.netlify.app">
    <img src="https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=netlify&logoColor=white" />
  </a>
  <a href="https://x.com/GonnabeNikhil">
    <img src="https://img.shields.io/badge/Twitter(X)-000000?style=for-the-badge&logo=twitter&logoColor=white" />
  </a>
</p>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=TryingtobeingNikhil&color=00ff41&style=flat-square&label=Profile+Views" alt="Profile Views">
</p>

<p align="center"><sub>⚡ Open to ML internships & full-time opportunities</sub></p>
<p align="center"><sub><i>P.S. If you've read this far, either my SEO worked or you're genuinely curious. Either way — hi, let's talk.</i></sub></p>
