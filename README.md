<p align="center">
  <img src="https://user-images.githubusercontent.com/61057666/169029838-74df663d-2e62-4d77-bdff-b43f7d63f00f.png" width="100%" />
</p>
<h1 align="center">Nikhil Mourya</h1>
<p align="center"><b>ML Engineer · Model Efficiency · Production NLP</b></p>
<p align="center"><i>I shrink models for a living. Production still finds a way to shrink me back.</i></p>

---

I work at the intersection of model compression and production ML — shrinking models without losing what they're for, then shipping them somewhere real. My projects aren't independent experiments; they're a single obsession with one question: *how much can you remove before the model stops being useful?*

---

Third year at BIT Mesra, studying what doesn't fit in a lecture hall.

---

Software Engineer — ML at [HireBuddy](https://www.hirebuddy.net) *(May–Nov 2025)* — built AI hiring infrastructure processing 10K+ resumes/day in production.
focus     : efficient LLMs · RAG systems · production ML pipelines
currently : open to ML internships & full-time opportunities
location  : Jaipur, India
cf        : Specialist 1400+

---

## What I Actually Build

My work follows a thread: **train lean, compress hard, ship it.**

| Project | The Question I Was Answering | Result |
|---|---|---|
| [CodeLens](https://github.com/TryingtobeingNikhil/CodeLens) | Can you search a codebase by intent, not keywords — fully offline? | VS Code extension, AST chunking, 9K+ chunks, sub-10ms search · [Demo ↗](https://youtu.be/d2I2omkHVLE) |
| [Agentic RAG Chatbot](https://github.com/TryingtobeingNikhil/Agentic-RAG-chatbot) | Can an LLM plan its own retrieval instead of just being handed chunks? | Multi-step retrieval, ReAct agent, query routing across 3 sources |
| [Pruned U-Net](https://github.com/TryingtobeingNikhil/Pruned-UNet-Biomedical-Segmentation) | How much of a segmentation model is actually load-bearing? | 97.3% params removed, IoU > 0.95 held · IIT Kharagpur |
| [PEGASUS + LoRA](https://github.com/TryingtobeingNikhil/pegasus-lora-efficient-summarization) | Can you fine-tune a 767M model on a student budget? | 99.8% param reduction, 27× faster training |
| [Vectorless RAGs](https://github.com/TryingtobeingNikhil/Vectorless-RAGs) | Is a vector database a requirement or just a habit? | Full retrieval pipeline, zero embeddings, zero vector DB |
| [AttentionIsALLICode](https://github.com/TryingtobeingNikhil/AttentionIsALLICode) | Do I actually understand attention, or just import it? | Full GPT-style LM, zero frameworks |

---

## Projects

### 🔍 CodeLens · Offline Semantic Code Search (VS Code Extension)
*Apr 2026 · [GitHub](https://github.com/TryingtobeingNikhil/CodeLens) · [Demo ↗](https://youtu.be/d2I2omkHVLE)*

**The problem:** You join a large codebase. You know there's *some* function that handles JWT token refresh — but `Ctrl+F "token"` returns 847 matches. Traditional search matches text, not intent.

**What I did:** Built a fully offline VS Code extension that indexes your codebase using AST-based chunking (tree-sitter) and 768-dim embeddings via Ollama. Natural language query → ranked semantic results → one-click jump to the exact line. No internet, no API keys, no cloud.

**Results:** 9K+ chunks indexed · sub-10ms ANN lookup · auto-reindexes on file save via MD5 hashing · optional Mistral 7B explain mode

`Python` `TypeScript` `FastAPI` `tree-sitter` `Ollama` `FAISS` `VS Code API` `Docker`

[→ View Repository](https://github.com/TryingtobeingNikhil/CodeLens) · [→ Watch Demo](https://youtu.be/d2I2omkHVLE)

---

### 🤖 Agentic RAG Chatbot · Adaptive Retrieval System
*Mar 2026 · [GitHub](https://github.com/TryingtobeingNikhil/Agentic-RAG-chatbot)*

**The problem:** Standard RAG pipelines are passive — they retrieve once and answer. Real queries often need multiple retrieval steps, context refinement, and the ability to recognize when the first answer wasn't good enough.

**What I did:** Built an adaptive RAG system with intelligent query routing across 3 sources — FAISS vector index, Groq LLM general knowledge, and Tavily web search. ReAct agent handles relevance grading and automatic query rewriting when retrieved docs don't pass the confidence threshold.

**What I learned:** The hard part isn't retrieval — it's knowing when to retrieve again.

`Python` `LangChain` `LangGraph` `FastAPI` `FAISS` `Streamlit` `Groq` `Tavily`

[→ View Repository](https://github.com/TryingtobeingNikhil/Agentic-RAG-chatbot)

---

### 🧬 Pruned U-Net · Biomedical Segmentation
*Mar 2025 · IIT Kharagpur research collaboration · [GitHub](https://github.com/TryingtobeingNikhil/Pruned-UNet-Biomedical-Segmentation)*

**The problem:** U-Net for biomedical segmentation is over-parameterized by design — built for generality, not efficiency. Most medical imaging deployments don't need that headroom.

**What I did:** Structured magnitude pruning pipeline targeting channels, not individual weights. The key insight was that IoU degraded sharply after ~96% reduction but had a long flat region before that — meaning there's a wide safe compression window most implementations never explore.

**Results:** 97.3% parameter reduction · 92% FLOPs reduction · IoU > 0.95 on MoNuSeg

`PyTorch` `U-Net` `Model Pruning` `Computer Vision` `MoNuSeg`

[→ View Repository](https://github.com/TryingtobeingNikhil/Pruned-UNet-Biomedical-Segmentation)

---

### 📝 PEGASUS + LoRA · Efficient Summarization
*Feb 2026 · [GitHub](https://github.com/TryingtobeingNikhil/pegasus-lora-efficient-summarization)*

**The problem:** Full fine-tuning a 767M parameter model requires compute most practitioners don't have.

**What I did:** Applied LoRA rank-decomposition adapters via HuggingFace PEFT on BBC XSum dataset, targeting attention weight matrices. Rank selection (r=16) was the critical decision — lower ranks trained faster but degraded ROUGE scores noticeably; higher ranks approached full fine-tuning cost.

**Results:** 767M → 1.57M trainable parameters (99.8% reduction) · 27× faster training (260s → 9.5s) · LoRA avoided catastrophic forgetting while full fine-tuning produced word salad on unseen domains.

`PyTorch` `HuggingFace` `PEFT` `LoRA` `NLP` `XSum`

[→ View Repository](https://github.com/TryingtobeingNikhil/pegasus-lora-efficient-summarization)

---

### 🔍 Vectorless RAGs
*Ongoing · [GitHub](https://github.com/TryingtobeingNikhil/Vectorless-RAGs)*

**The problem:** Vector databases have become the default assumption in RAG architectures. I wanted to know if that default is load-bearing or just conventional.

**What I did:** Full RAG pipeline using LLM-guided tree traversal — no embeddings, no vector index, no similarity search. Performs well on structured, domain-specific corpora; degrades on semantically ambiguous queries where dense retrieval has a real advantage.

*Half the RAG stacks I meet are a vector DB cosplaying as a product requirement.*

`Python` `Ollama` `LLaMA 3` `RAG` `Tree Traversal` `Streamlit`

[→ View Repository](https://github.com/TryingtobeingNikhil/Vectorless-RAGs)

---

### 🔤 AttentionIsALLICode · GPT Transformer from Scratch
*Oct 2025 · [GitHub](https://github.com/TryingtobeingNikhil/AttentionIsALLICode)*

**The problem:** Most people use transformers. Fewer understand what's actually happening inside the attention computation.

**What I did:** Full GPT-style character-level language model in raw PyTorch trained on Tiny Shakespeare — multi-head self-attention, causal masking, positional encoding, residual connections, layer norm, custom training loop with gradient clipping and cosine LR schedule.

`PyTorch` `Transformers` `NLP` `From Scratch`

[→ View Repository](https://github.com/TryingtobeingNikhil/AttentionIsALLICode)

---

## Production Experience

**Software Engineer — Machine Learning · [HireBuddy](https://www.hirebuddy.net)** *(May 2025 – Nov 2025)*

Built the ML infrastructure from zero — India-specific resume scoring system via transformer embeddings and RAG pipelines, improving shortlist precision by 35% over keyword-matching baseline. NLP pipelines for job-fit scoring and candidate ranking via LangChain. FastAPI + Docker deployment on GCP Cloud Run with REST API integration into recruiter workflows, increasing platform engagement by 40%. Processed 10K+ resumes/day in production.

Key decisions: chunking strategy for resume parsing, reranking pipeline design, latency vs accuracy tradeoff for real-time scoring.

---

## Hackathons

**Smart India Hackathon 2024 · Finalist**
ML-based hospital queue prioritization — 28% predicted wait time reduction. Flask APIs on GCP. The constraint that made it interesting: the model had to be explainable to non-technical hospital staff, not just accurate.

**IIIT Delhi Hackathon 2023 · Finalist**
ResNet50 classifier, 94% accuracy, 30% training time reduction via mixed-precision training. The win came from profiling the data loading bottleneck, not the model itself.

---

## Skills

**Core:** Python · C++ · PyTorch · TensorFlow · HuggingFace · Scikit-learn  
**LLMs & RAG:** LangChain · LangGraph · PEFT · LoRA · Transformers · RAG Pipelines · OpenAI API  
**Deployment:** FastAPI · Flask · Docker · GCP (Cloud Run) · REST APIs  
**Data:** NumPy · Pandas · Matplotlib · SQL · W&B  
**CP:** C++ · Codeforces Specialist (1400+)  

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

<p align="center"><sub>⚡ Open to ML internships & full-time opportunities in model efficiency and production NLP</sub></p>
<p align="center"><sub><i>P.S. If you've read this far, either my SEO worked or you're genuinely curious. Either way — hi, let's talk.</i></sub></p>
