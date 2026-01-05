# 🧠 TheoremLabs R&D Spike — Hybrid Knowledge Strategy

## 1. Spike Overview

| Field | Entry |
| :--- | :--- |
| **Spike ID** | `SPK-009-ElevenLabs-Hybrid-Knowledge` |
| **Title** | **Advanced Knowledge Injection: System Prompt vs. Custom RAG Strategy** |
| **Category** | `AI Engineering / Backend` |
| **Created by** | TheoremLabs Applied Innovation Labs |
| **Start Date** | *Immediate* |
| **Status** | Proposed |
| **Tags** | `Next.js`, `Fastify`, `ElevenLabs Knowledge Base`, `Vector Stores`, `RAG` |

---

## 2. Purpose & Hypothesis

### Purpose
Standard Retrieval Augmented Generation (RAG) often fragments context, causing agents to miss the "Big Picture" of a domain. While ElevenLabs offers a native Knowledge Base, it may lack the granularity or control required for complex use cases.

This spike requires the candidate to **architect the "Brain" of the agent**. You must evaluate the native ElevenLabs storage against a **Custom Knowledge Store** (using your choice of vector database/indexing strategy) and design a **Hybrid Pipeline** that intelligently routes data—deciding when to inject "God Mode" context directly into the System Prompt vs. when to offload data to an external or native store.

### Hypothesis
> “To ensure the agent has 'knowledge of everything' in a specific domain, we cannot rely solely on native retrieval tools. A hybrid approach—combining direct System Prompt injection for critical constraints with a high-precision Custom RAG (or optimized Native RAG) for reference data—will yield higher accuracy and lower hallucination rates.”

---

## 3. Experiment / Research Method

You are free to design the implementation details. Your goal is to deliver a validated strategy that answers the following:

### Key Objectives

1.  **Analyze & Benchmark Storage Options:**
    * Evaluate the **ElevenLabs Native Knowledge Base**: How does it handle chunking? What is its retrieval latency and accuracy?
    * Prototype a **Custom Knowledge Store** (optional but recommended): Would a custom vector solution (e.g., Pinecone, Pgvector, Weaviate) allow for better chunking strategies or semantic search accuracy?

2.  **Architect the Ingestion Pipeline:**
    * Design the logic that sits in the Fastify backend to process uploaded files.
    * Determine the heuristic: *When* should a file be forced into the System Prompt (Context Injection) versus stored in a RAG system? (Consider file size, token limits, and information density).

3.  **Validate the "Hybrid" Logic:**
    * Create a test scenario where an agent must synthesis information from multiple parts of a document.
    * Compare the performance of:
        * Pure Native RAG.
        * Pure Custom RAG.
        * The Hybrid Approach (Prompt Injection + Storage).

### Output Typologies

| Output Type | Expectation |
| :--- | :--- |
| **Strategy Document** | A definitive guide: "Use Native KB when X, use Custom Store when Y, use Prompt Injection when Z." |
| **Architecture Diagram** |  Visualizing the flow of data from Upload $\to$ Parser $\to$ Storage/Prompt. |
| **Proof of Concept** | Functional code in Fastify that implements your chosen ingestion strategy. |

---

## 4. Tools, Data & References

| Type | Example Entry |
| :--- | :--- |
| **Stack** | Next.js (Frontend), Fastify (Backend) |
| **Options** | ElevenLabs Knowledge Base API, LangChain, Pinecone, Qdrant |
| **References / Docs** | [11Labs: Knowledge Base API](https://elevenlabs.io/docs/api-reference/knowledge-base) |

---

## 5. Findings / Observations

Document what you discover. Some mock example findings:

- **Native Limitations:** "Native RAG chunking was too aggressive, breaking tables across chunks. We recommend a custom parser for financial documents."
- **Accuracy Wins:** "Custom RAG with 'Parent Document Retrieval' outperformed ElevenLabs Native RAG by 20% on multi-hop questions."
- **Latency Trade-offs:** "Injecting 15k tokens into the System Prompt increased initial latency by 600ms but eliminated hallucinations completely."

Include any code snippets, screenshots, logs, or charts in `/assets/` or logs in `/notes/`.

---

## 6. Conclusion & Recommendations

| Decision | Notes |
| :--- | :--- |
| ✅ Adopt | [Your recommendation on whether to stick with Native or build Custom] |
| 🔁 Iterate | [Areas where the retrieval accuracy needs tuning] |
| 🚫 Reject | N/A |

**Recommendation:**
Provide a clear recommendation on the final architecture. Should we avoid the Native KB entirely in favor of a custom solution? Or is the Native KB sufficient for 80% of use cases?

---

## 7. Related Spikes / References
- [SPK-008: Agent Control Plane] (The dashboard where this functionality will live)
- [Video: RAG vs Context Window](https://www.youtube.com/watch?v=2IK3DFHRFfw) (Concept refresher)

---

## 8. Attachments

Place any support files here:

- `/backend/` → Fastify source code (Ingestion & Retrieval Logic)
- `/frontend/` → Next.js source code (Upload UI)
- `/docs/` → "Storage Benchmark: Native vs Custom"
- `/logs/` → Chat transcripts comparing accuracy

---

## 9. TL;DR Summary

This spike focuses on the **Brain** of the agent. You must determine the best way to store and retrieve domain knowledge. You will evaluate the **ElevenLabs Native Knowledge Base** against **Custom RAG implementations** and design a backend pipeline that intelligently routes data—either injecting it directly into the System Prompt for total recall or storing it in a vector database for efficient reference—to maximize agent accuracy.

---

*Notes / Tips:*

- Keep each spike **bounded in time** (ideally ≤ 7 days)
- Code for **“just enough” to learn** — don’t over-engineer
- Document **failures and gaps** — they’re just as valuable
- Use clear naming: example folder name `spk-009-Hybrid-Knowledge`

Good luck!
contact author of this spike: research@theoremlabs.io
