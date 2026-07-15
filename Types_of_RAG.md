# Types of RAG (Retrieval-Augmented Generation)
# ponytail: from naive to advanced — each type solves a specific failure mode

## Evolution Overview

```
Naive RAG (2020)
  └── Basic: retrieve → augment → generate
       |
       ├── Advanced RAG (2023)
       │    ├── Pre-retrieval: optimize query/chunks BEFORE search
       │    └── Post-retrieval: rerank/compress AFTER search
       │
       ├── Modular RAG (2024)
       │    └── Plug-and-play components: search, rewrite, filter, fuse
       │
       └── Agentic RAG (2024-2025)
            └── LLM decides WHEN and HOW to retrieve (tools, loops, multi-step)
```

---

## 1. Naive RAG (The Original)

```
Query → Retrieve (similarity search) → Feed chunks + Query → LLM generates answer
```

The simplest form. Embed the query, find top-k similar chunks, stuff them into a prompt.

**Problems:**
- One-shot retrieval — no refinement
- Fixed chunk size — may split critical context
- No query rewriting — bad queries get bad results
- No reranking — top-k by similarity may miss relevant docs

**Best for:** Prototyping, simple Q&A on clean documents.

---

## 2. Advanced RAG — Pre-Retrieval Optimization

### 2a. Query Rewriting / Expansion

Rewrite the user's query BEFORE searching to improve retrieval quality.

```python
from langchain_core.prompts import ChatPromptTemplate

rewriter = (
    ChatPromptTemplate.from_template(
        "Rewrite this question to be more specific for document search:\n{query}")
    | llm | StrOutputParser()
)
better_query = rewriter.invoke("tell me about LoRA")
# "What is Low-Rank Adaptation (LoRA) and how does it work for fine-tuning LLMs?"
```

**Techniques:**
- **Query rewriting**: LLM rephrases vague queries
- **Multi-query**: generate N query variations, retrieve for each, merge results
- **HyDE** (Hypothetical Document Embeddings): generate a fake answer, embed that instead

### 2b. Chunking Strategies

```
Bad chunking:     "LoRA is a... technique that..." | "fine-tunes large... models..."
Good chunking:    "LoRA is a technique that fine-tunes large models..." (complete thought)
```

| Strategy                    | How it works                              | Best for                     |
|-----------------------------|-------------------------------------------|------------------------------|
| Recursive Character Split   | Split on \n\n → \n → . → space            | General text                 |
| Semantic Splitter            | Split at topic boundaries (embedding diff)| Articles with clear sections |
| Token-based Split           | Split by token count                      | Code, structured text        |
| Agentic Split               | LLM decides where to split                | Maximum precision            |
| Sentence Window Split       | Keep N sentences around each chunk        | Need context on both sides   |

### 2c. Metadata Filtering

Filter documents BEFORE similarity search using metadata:
```python
retriever = vectorstore.as_retriever(
    search_kwargs={"k": 3, "filter": {"year": 2024, "category": "deep-learning"}}
)
```

---

## 3. Advanced RAG — Post-Retrieval Optimization

### 3a. Reranking

Retrieve MORE docs (e.g., k=20), then rerank with a cross-encoder for precision.

```python
from langchain.retrievers import ContextualCompressionRetriever
from langchain.retrievers.document_compressors import CrossEncoderReranker
from langchain_community.cross_encoders import HuggingFaceCrossEncoder

reranker = CrossEncoderReranker(
    model=HuggingFaceCrossEncoder(model_name="BAAI/bge-reranker-v2-m3"),
    top_n=3,
)
compression_retriever = ContextualCompressionRetriever(
    base_compressor=reranker,
    base_retriever=vectorstore.as_retriever(search_kwargs={"k": 20}),
)
```

**Why?** Bi-encoder (embedding) is fast but approximate. Cross-encoder is slow but precise. Combine both: fast recall + precise rerank.

### 3b. Contextual Compression

Retrieve docs, then compress/trim each doc to keep ONLY the relevant parts.

```python
from langchain.retrievers.document_compressors import LLMChainExtractor

compressor = LLMChainExtractor.from_llm(llm)
compression_retriever = ContextualCompressionRetriever(
    base_compressor=compressor,
    base_retriever=vectorstore.as_retriever(),
)
```

### 3c. Prompt Compression

Compress the ENTIRE retrieved context into a shorter representation:
- **LLMLingua**: uses a small LM to remove tokens that don't affect the answer
- **Selective Context**: keep only sentences containing query keywords

---

## 4. Modular RAG

Plug-and-play components. You can ADD or REMOVE stages without rewriting.

```
Query ──→ Rewrite ──→ Retrieve ──→ Rerank ──→ Compress ──→ Generate
              ↑                         ↑
         (optional)                 (optional)
```

**Modules:**
- Search: dense vector, sparse (BM25), hybrid
- Query Transformation: rewrite, expand, HyDE
- Routing: send different query types to different retrievers
- Fusion: RRF (Reciprocal Rank Fusion) merges multiple result sets
- Memory: use chat history for context-aware retrieval
- Filter: metadata filter, timestamp filter

**Best for:** Production systems where you need to tune each stage independently.

---

## 5. Agentic RAG

The LLM ACTS as an agent that decides HOW and WHEN to retrieve.

```
User → Agent → Decide → [Retrieve, Search Web, Calculate, Ask follow-up] → Answer
                         ↑
                    (loops until done)
```

```python
from langchain.agents import create_tool_calling_agent, AgentExecutor
from langchain.tools.retriever import create_retriever_tool

tool = create_retriever_tool(
    retriever,
    name="search_docs",
    description="Search through the documentation. Use for any technical questions.",
)
agent = create_tool_calling_agent(llm, [tool], prompt)
executor = AgentExecutor(agent=agent, tools=[tool])
executor.invoke({"input": "What is LoRA and how does it compare to QLoRA?"})
```

**Capabilities:**
- Multi-step: retrieve → read → retrieve more → synthesize
- Tool-use: search docs, run code, calculate, search web
- Reflection: if answer is weak, rephrase and search again
- Adaptive: adjust chunk size, k value, or search strategy based on query

**Best for:** Complex questions, multi-hop reasoning, research assistance.

---

## 6. Advanced RAG Variants

### 6a. Hierarchical RAG

Two-level retrieval: summary-level first, then detail-level.

```
Query → Find relevant summaries (coarse) → Fetch full chunks (fine) → Answer
```

**Why?** Reduces retrieval space. Summary index is small, fast. Full chunks are large, precise.

### 6b. Multi-Hop RAG

Answer requires information from MULTIPLE documents that build on each other.

```
Query: "What is the impact of LoRA on transformer inference speed?"
  Hop 1: "What is LoRA?" → chunk about LoRA technique
  Hop 2: "How does LoRA affect transformer inference?" → chunk about inference
  Hop 3: "What are the speed measurements?" → chunk with benchmarks
  Final: Synthesize all three
```

**Best for:** Research questions, analysis, comparison queries.

### 6c. Graph RAG

Build a knowledge graph from documents, then retrieve by traversing relations.

```
Documents → Extract entities + relations → Build graph → Query traverses graph → Answer
```

**Why?** Captures relationships between concepts that vector similarity misses.
*Example: "How does LoRA relate to quantization?" requires knowing LoRA ≠ Quantization,
but they're both efficiency techniques — graph captures this relation.*

**Best for:** Multi-entity questions, relationship-heavy domains (medical, legal).

### 6d. Self-RAG

The LLM generates special tokens to DECIDE whether retrieval is needed.

```
Input → LLM generates
  [Retrieve] token? YES → search → augment → generate
                     NO  → generate from knowledge alone
  [Critique] token → check if answer is supported by retrieved context
```

**Why?** Not every question needs retrieval. Self-RAG saves cost and latency when
the LLM already knows the answer. Also adds self-critique for factuality.

### 6e. Corrective RAG (CRAG)

If retrieved chunks have LOW relevance, the system CORRECTS instead of using them blindly.

```
Retrieve → Evaluate relevance → If low: search web or rewrite query
                                 If medium: keep, but narrow
                                 If high: use as-is
```

**Why?** Vanilla RAG fails silently on bad retrievals. CRAG catches and corrects them.

### 6f. Fusion RAG (RRF — Reciprocal Rank Fusion)

Run MULTIPLE retrievers in parallel, merge results with RRF scoring.

```python
from langchain.retrievers import EnsembleRetriever
from langchain_community.retrievers import BM25Retriever

# Dense retriever (vector search)
dense_retriever = vectorstore.as_retriever(search_kwargs={"k": 5})

# Sparse retriever (keyword search)
sparse_retriever = BM25Retriever.from_documents(chunks)
sparse_retriever.k = 5

# Ensemble both
ensemble = EnsembleRetriever(
    retrievers=[dense_retriever, sparse_retriever],
    weights=[0.5, 0.5],  # equal weight
)
results = ensemble.invoke("LoRA fine-tuning")
# Combines: vector similarity + keyword matching = best of both worlds
```

**Why?** Dense retrieval misses exact keyword matches. Sparse (BM25) misses semantic matches. Together they catch both.

### 6g. HyDE (Hypothetical Document Embeddings)

Instead of embedding the query, ask the LLM to GENERATE a fake answer document,
then embed THAT document and search.

```
Query: "Explain LoRA rank parameter"
  → LLM generates: "LoRA rank (r) controls the bottleneck dimension..."
  → Embed the generated text
  → Search with that embedding
```

**Why?** Query (short, vague) and documents (long, specific) live in different
embedding spaces. HyDE bridges the gap by converting the query into document-like text.

---

## Comparison Table

| RAG Type          | When to Use                                       | Complexity | Quality Gain |
|-------------------|---------------------------------------------------|------------|--------------|
| Naive RAG         | Quick prototype, clean docs                       | ⭐         | Baseline     |
| Query Rewriting   | Users ask vague questions                         | ⭐⭐       | +20-30%      |
| Reranking         | Need high precision, have many candidates         | ⭐⭐       | +15-25%      |
| Multi-Query       | Query is ambiguous, need coverage                 | ⭐⭐       | +20-40%      |
| HyDE              | Queries are short, documents are long             | ⭐⭐       | +10-20%      |
| Agentic RAG       | Complex multi-step questions, need tool-use       | ⭐⭐⭐⭐    | +30-50%      |
| Graph RAG         | Multi-entity, relationship-heavy domain           | ⭐⭐⭐⭐⭐   | +40-60%      |
| Self-RAG          | Mixed query types, want to save cost              | ⭐⭐⭐      | +10-30%      |
| Corrective RAG    | Noisy data, high cost of bad answers              | ⭐⭐⭐      | +20-40%      |
| Fusion (Hybrid)   | Need both semantic + keyword search               | ⭐⭐       | +15-30%      |
| Hierarchical RAG  | Very large document corpus (millions of docs)     | ⭐⭐⭐      | +10-20%      |
| Multi-Hop RAG     | Questions require reasoning across multiple docs   | ⭐⭐⭐⭐    | +30-50%      |

---

## Quick Decision Flowchart

```
How complex is the query?
│
├─ Simple fact lookup ──────────────→ Naive RAG 🟢
│
├─ Vague / poorly worded ───────────→ Query Rewriting + Multi-Query 🟢
│
├─ Needs both keyword + meaning ────→ Fusion (Hybrid Search) 🟢
│
├─ Needs high precision ────────────→ Reranking 🟢
│
├─ Multi-step / compare / analyze ──→ Agentic RAG or Multi-Hop 🟡
│
├─ Relationship-heavy (medical/legal) → Graph RAG 🟠
│
├─ Huge corpus (10M+ docs) ─────────→ Hierarchical RAG 🟠
│
└─ Cost-sensitive, mixed queries ───→ Self-RAG + Corrective RAG 🟡
```
