<p align="center">
  <img src="https://user-images.githubusercontent.com/61057666/169029838-74df663d-2e62-4d77-bdff-b43f7d63f00f.png" width="100%" />
</p>

<h1 align="center">Nikhil Mourya</h1>
<p align="center"><b>ML Engineer · Model Efficiency · Production NLP</b></p>
<p align="center"><i>I shrink models for a living. Production still finds a way to shrink me back.</i></p>

---

I work at the intersection of model compression and production ML — shrinking models without losing what they're for, then shipping them somewhere real. My projects aren't independent experiments; they're a single obsession with one question: *how much can you remove before the model stops being useful?*

---

Debugging life at BIT Mesra...

---

Founding ML Member at [HireBuddy](https://www.hirebuddy.net) — building AI hiring infrastructure that processes 10K+ resumes/day in production.

```
focus     : efficient LLMs · RAG systems · production ML pipelines
currently : open to Summer 2026 ML internships & research collaborations
location  : Jaipur, India
cf        : Specialist 1400+
```

---

## What I Actually Build

My work follows a thread: **train lean, compress hard, ship it.**

| Project | The Question I Was Answering | Result |
|---|---|---|
| [Agentic RAG Chatbot](#-agentic-rag-chatbot--autonomous-retrieval-system) | Can an LLM plan its own retrieval instead of just being handed chunks? | Multi-step retrieval with iterative reasoning & query rewriting |
| [Pruned U-Net](#-pruned-u-net--biomedical-segmentation) | How much of a segmentation model is actually load-bearing? | 97.3% params removed, IoU > 0.95 held |
| [PEGASUS + LoRA](#-pegasus--lora--efficient-summarization) | Can you fine-tune a 767M model on a student budget? | 99.8% param reduction, 27× faster training |
| [AttentionIsALLICode](#-attentionisallicode--gpt-transformer-from-scratch) | Do I actually understand attention, or just import it? | Full GPT-style LM, zero frameworks |
| [Vectorless RAGs](#-vectorless-rags) | Is a vector database a requirement or just a habit? | Full retrieval pipeline, zero embeddings, zero vector DB |

---

## Projects

### 🤖 Agentic RAG Chatbot · Autonomous Retrieval System
*2026*

**The problem:** Standard RAG pipelines are passive — they retrieve once and answer. Real queries often need multiple retrieval steps, context refinement, and the ability to recognize when the first answer wasn't good enough.

**What I did:** Built an agentic RAG system with autonomous query planning, multi-step retrieval, and iterative reasoning. Integrated LLMs with a vector DB and tool-calling; added memory and query rewriting to improve answer relevance across turns.

**What I learned:** The hard part isn't retrieval — it's knowing when to retrieve again. Getting the agent to recognize low-confidence states and replan is where most of the engineering effort went.

`Python` `LangChain` `LangGraph` `LLMs` `Vector DB` `RAG`

[→ View Repository](https://github.com/TryingtobeingNikhil/Agentic-RAG-Chatbot)

---

### 🧬 Pruned U-Net · Biomedical Segmentation
*IIT Kharagpur collaboration · Mar 2025*

**The problem:** U-Net for biomedical segmentation is over-parameterized by design — built for generality, not efficiency. Most medical imaging deployments don't need that headroom.

**What I did:** Structured magnitude pruning pipeline targeting channels, not individual weights. The key insight was that IoU degraded sharply after ~96% reduction but had a long flat region before that — meaning there's a wide safe compression window most implementations never explore.

**Results:** 97.3% parameter reduction · 92% FLOPs reduction · IoU > 0.95 on MoNuSeg · Fully config-reproducible

**What surprised me:** The model was more robust to pruning than expected up to a threshold, then collapsed quickly. The threshold, not the pruning method, is what actually matters to tune.

`PyTorch` `TensorFlow` `U-Net` `Model Pruning` `Computer Vision` `MoNuSeg`

[→ View Repository](https://github.com/TryingtobeingNikhil/Pruned-U-Net)

---

### 📝 PEGASUS + LoRA · Efficient Summarization
*Feb 2026*

**The problem:** Full fine-tuning a 767M parameter model requires compute most practitioners don't have. The question is whether LoRA adapters can close that gap without meaningful quality loss.

**What I did:** Applied rank-decomposition adapters via HuggingFace PEFT, targeting attention weight matrices. Rank selection (r=16) was the critical decision — lower ranks trained faster but degraded ROUGE scores noticeably; higher ranks approached full fine-tuning cost. Served via FastAPI with Docker packaging.

**Results:** 767M → 1.57M trainable parameters (99.8% reduction) · 27× faster training · FastAPI endpoint · Docker packaged

*Because training 767M parameters is expensive, and I'm not Google.*

`PyTorch` `HuggingFace` `PEFT` `LoRA` `FastAPI` `Docker` `NLP`

[→ View Repository](https://github.com/TryingtobeingNikhil/PEGASUS-LoRA)

---

### 🔤 AttentionIsALLICode · GPT Transformer from Scratch
*Oct 2025*

**The problem:** Most people use transformers. Fewer understand what's actually happening inside the attention computation.

**What I did:** Full GPT-style language model in raw PyTorch — multi-head self-attention, causal masking, positional encoding, residual connections, layer norm. Custom training loop with gradient clipping and cosine LR schedule.

**What I learned:** The gap between "I understand attention" and "I can implement attention and debug why it's not training" is significant. Residual connections matter more than most tutorials suggest.

`PyTorch` `Transformers` `NLP` `From Scratch`

[→ View Repository](https://github.com/TryingtobeingNikhil/AttentionIsALLICode)

---

### 🔍 Vectorless RAGs
*Ongoing*

**The problem:** Vector databases have become the default assumption in RAG architectures. I wanted to know if that default is load-bearing or just conventional.

**What I did:** Full RAG pipeline using tree traversal and keyword-based retrieval — no embeddings, no vector index, no similarity search. Uses Ollama + LLaMA 3 locally. Performs well on structured, domain-specific corpora; degrades on semantically ambiguous queries where dense retrieval has a real advantage.

*Half the RAG stacks I meet are a vector DB cosplaying as a product requirement.*

`Python` `Ollama` `LLaMA 3` `RAG` `Tree Traversal` `Streamlit`

[→ View Repository](https://github.com/TryingtobeingNikhil/Vectorless-RAGs)

---

## Production Experience

**Founding ML Member · [HireBuddy](https://www.hirebuddy.net)** *(May 2025 – Nov 2025)*

Built the ML infrastructure from zero — resume-job matching via transformer-based embeddings and RAG pipelines, improving shortlist precision by 35%. NLP pipelines for job-fit scoring and candidate ranking via LangChain. Flask + Docker deployment on GCP Cloud Run with REST API integration into recruiter workflows, increasing platform engagement by 40%. The system processes 10K+ resumes/day in production.

Key decisions: chunking strategy for resume parsing, reranking pipeline design, latency vs accuracy tradeoff for real-time scoring.

---

## Hackathons

**Smart India Hackathon 2024 · Finalist**
ML-based hospital queue prioritization — 28% predicted wait time reduction. Flask APIs on GCP. The constraint that made it interesting: the model had to be explainable to non-technical hospital staff, not just accurate.

**IIIT Delhi Hackathon 2024 · Finalist**
ResNet50 classifier, 94% accuracy, 30% training time reduction via mixed-precision training. The win came from profiling the data loading bottleneck, not the model itself.

---

## Skills

**Core:** Python · C++ · PyTorch · TensorFlow · HuggingFace · Scikit-learn
**LLMs & RAG:** LangChain · LangGraph · PEFT · LoRA · Transformers · RAG Pipelines · OpenAI API
**Deployment:** FastAPI · Flask · Docker · GCP (Cloud Run) · REST APIs
**Data:** NumPy · Pandas · Matplotlib · SQL
**Foundations:** DSA · Linear Algebra · Probability · Statistics
**CP:** C++ · Codeforces Specialist (1400+)

---

## Achievements

- 🥇 Finalist — Smart India Hackathon 2024
- 🥇 Finalist — IIIT Delhi Hackathon 2024
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

<p align="center"><sub>⚡ Open to Summer 2026 ML internships & research collaborations in model efficiency and production NLP</sub></p>

<p align="center"><sub><i>P.S. If you've read this far, either my SEO worked or you're genuinely curious. Either way — hi, let's talk.</i></sub></p>
