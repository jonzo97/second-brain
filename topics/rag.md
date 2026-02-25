# RAG & Knowledge Graphs

Retrieval-augmented generation and knowledge graph tools.

## RAG Implementations

- [ ] [RAGify](https://github.com/kanad13/RAGify) - Chat with your documents using GenAI & RAG
- [ ] [UniversalRAG](https://universalrag.github.io/) - RAG over corpora of diverse modalities and granularities

## Knowledge Graphs

- [ ] [knowledge_graph](https://github.com/rahulnyk/knowledge_graph) - Convert any text to a graph of knowledge, for Graph Augmented Generation or KG-based QnA

## Research Topics

- [ ] [rag-cli](https://github.com/ItMeDiaTech/rag-cli) — Local RAG using Chroma vector embeddings for Claude Code
- [ ] Direct-code RAG recipe — Skip MCP, use Python + ChromaDB directly (pattern at ~/cc_agents/recipes/chromadb.md)
- [x] GraphRAG — **ANSWERED (research #02, #04):** GraphRAG is a spectrum: Microsoft full pipeline (enterprise, $33K+) → skeleton indexing (FalkorDBLite, practical) → wikilink-boost scoring (near-zero overhead). For <10K docs, use skeleton indexing or 3-step hybrid (vector seed → graph traverse → serialize). See Graph Database section below.
- [x] RAG evaluation frameworks — **ANSWERED (research #04):** RAGAS RAG Triad (Context Relevance, Groundedness, Answer Relevance). Must align judge LLM on 20+ manual samples first. Alternative: DeepEval.
- [x] Hybrid search patterns — **ANSWERED (research #04):** Dense vector + BM25 sparse fused via Reciprocal Rank Fusion (RRF, k=60). ChromaDB 2026 has first-class RRF + sparse index support.
- [x] Embedding model comparison 2026 — **ANSWERED (research #04):** Qwen3-Embedding-0.6B/4B (SOTA, 32K ctx, instruction-aware) > BGE-M3 (8K ctx, unified modes) > all-MiniLM-L6-v2 (obsolete). For code: Nomic Embed Code (7B). Multimodal: Jina v4.5.
- [ ] Project-specific knowledge bases — Indexed docs, past decisions, codebase patterns per project. Feed into agent context at session start.
- [ ] Cross-project memory via knowledge graph — Patterns, decisions, and learnings that apply across repos. Graph-db approach (see learning.md) or shared MCP memory server.
- [ ] Deep research workflow — Repeatable prompt→ingest→squeeze→PRD→execute cycle. Pattern at `~/cc_agents/docs/deep-research-workflow.md`

---

## Graph Database Evaluation (Research #02, Feb 2026)
*Source: extract_graph_databases.md*

### Database Comparison

| DB | Type | Fit | Notes |
|----|------|-----|-------|
| **CozoDB** (`pycozo`) | Embedded relational+graph+vector | **Recommended** | Single file, time-travel queries, Datalog, could replace ChromaDB |
| **DuckDB + PGQ** | SQL + graph extension | Alternative | Good if already using DuckDB for analytics |
| **FalkorDBLite** | Embedded graph | Lightweight GraphRAG | Python-only, skeleton indexing for PKM |
| **NetworkX** | In-memory graph | Transient analysis only | Use for PageRank/community detection, not persistence |
| **Kùzu** | Embedded graph | **AVOID** | Repo archived Oct 2025. Community fork "Bighorn" unproven |
| **Neo4j** | Server graph | Overkill for solo dev | Operational overhead not justified for local-first work |

### GraphRAG Retrieval Pattern (3-Step)
```
1. Vector seed → find 2-5 starting nodes via embedding similarity
2. Graph traverse → depth-limited (2-3 hops) from seeds, filter by relationship type
3. Serialize → extract sub-graph to structured text, token-budgeted for LLM context
```

### Key Constraints
- Limit traversal to 2-3 hops max for real-time agent use
- Token-budget graph results before returning to LLM — never dump raw sub-graphs
- Entity resolution MUST happen at ingestion time (not query time) — "Vivado" vs "Xilinx Vivado" = duplicate nodes
- Vector-only retrieval is structurally unsafe for engineering workflows (finds syntactically similar but architecturally wrong results)

### Tools & Reference Implementations
- [ ] [CozoDB](https://github.com/cozodb/cozo) (`pip install pycozo`) — unified embedded graph+vector+relational store
- [ ] [CocoIndex](https://github.com/cocoindex) (`pip install cocoindex`) — incremental markdown-to-graph ingestion
- [ ] [Mem0](https://github.com/mem0ai/mem0) (`pip install mem0ai`) — hybrid vector+graph memory, self-hosted
- [ ] [Zep](https://github.com/getzep/zep) — temporal knowledge graph, tracks fact changes over time
- [ ] [CodeGraphContext](https://www.reddit.com/r/mcp/) — MCP server indexing local code into graph DB
- [ ] `Lenny's Memory` (Neo4j Labs) — 3-tier memory: short-term, long-term, reasoning traces
- [ ] `M3-Agent` (arXiv 2508.09736) — multimodal agent with entity-centric graph memory

### Open Questions (Graph)
- [ ] CozoDB production maturity — is `pycozo` stable enough for core agent memory?
- [ ] Can CozoDB's integrated vector search fully replace ChromaDB?
- [ ] Does a community MCP server exist for CozoDB, or do we need to build one?
- [ ] Supernode detection — what tooling exists to identify and decompose highly-connected nodes?
- [ ] Establish ChromaDB-only retrieval accuracy baseline before adding graph layer

---

## RAG Best Practices 2026 (Research #04, Feb 2026)
*Source: extract_rag_best_practices.md*

### Current Recommended Stack (<10K docs, local-first)

| Component | Recommendation | Install |
|-----------|---------------|---------|
| **Embedding** | `Qwen3-Embedding-0.6B` (efficiency) or `4B` (quality) | `huggingface-hub` or Ollama |
| **Code embedding** | `Nomic Embed Code` (7B) | `huggingface-hub` |
| **Chunking** | Recursive character, 512 tokens, 15% overlap, code-aware separators | LangChain or custom |
| **Search** | Hybrid vector + BM25, fused via RRF (k=60) | ChromaDB 2026 |
| **Reranking** | `bge-reranker-v2-m3` (279M) or `Qwen3-Reranker-0.6B` (+15.4%) | `sentence-transformers` |
| **Graph layer** | Optional: `FalkorDBLite` skeleton indexing | `pip install falkordb` |
| **Evaluation** | RAGAS RAG Triad + manual judge alignment (20+ samples) | `pip install ragas` |

### Key Anti-Patterns (Performance Paradox)
- **Semantic chunking scores WORSE than recursive splitting** (60% vs 69% accuracy). It isolates function definitions from class context, impoverishing the generator's understanding.
- **all-MiniLM-L6-v2 is obsolete** for technical domains. Short context window can't ingest full source files.
- **Don't trust raw cosine similarity scores** as absolute thresholds. Score meaning is collection-specific. Use reranker or RRF instead.
- **Don't skip evaluation.** Most solo developers never implement systematic evaluation — pipeline regressions go unnoticed.
- **Full Microsoft GraphRAG is overkill at <10K docs.** Designed for millions of docs, costs $33K+ in LLM extraction. Use skeleton indexing instead.

### Embedding Model Comparison

| Model | Params | Context | Best For | Notes |
|-------|--------|---------|----------|-------|
| Qwen3-Embedding-0.6B | 600M | 32K | General (efficiency) | #1 MTEB, instruction-aware, Matryoshka |
| Qwen3-Embedding-4B | 4B | 32K | General (quality) | Same capabilities, more VRAM |
| BGE-M3 | 600M | 8K | Unified retrieval modes | Dense+sparse+multi-vector, ONNX 3x CPU speedup |
| Nomic Embed Code | 7B | — | Code | Rivals closed-source on code tasks |
| Jina v4.5 | 3B | — | Multimodal (text+code+diagrams) | Uses Qwen2.5-VL-3B, handles visual content |
| EmbeddingGemma-300M | 300M | — | Ultra-lightweight/mobile | On-device deployment |

### Community Implementations
- [ ] [ObsidianRAG](https://github.com/Vasallo94/ObsidianRAG) — Obsidian vault + Ollama + hybrid search + BGE-M3 reranker
- [ ] [graph-rag-workshop](https://github.com/kuzudb/graph-rag-workshop) — Kùzu + LanceDB hybrid graph+vector
- [ ] DuckDB-RAG — DuckDB VSS extension for local vector search over Markdown. Graph-boosted scoring (1.2x multiplier for wikilink-connected notes)
- [ ] [Pathway](https://pathway.com/) — Real-time incremental indexing for dynamic/live data

### Open Questions (RAG 2026)
- [ ] Which ChromaDB version added first-class sparse vector + RRF support? Need version pin.
- [ ] ObsidianRAG weight split (60% vector / 40% BM25) — better than equal RRF? Benchmark on real corpus.
- [ ] At what scale does FalkorDBLite skeleton indexing break down?
- [ ] Qwen3-Reranker-0.6B +15.4% over BGE — on what benchmark? Verify for technical docs.
