

# 🧪 TheoremLabs R&D Spike — Common TheoremLabs AI-Diagraming Shared Capability (TDC)

> A Research Spike to explore, evaluate, and architect a shared AI-Diagraming capability across TheoremLabs’ AI-Agent ecosystem.  
> This capability will generate visual, audio, or video outputs from human–AI conversational transcripts (.vtt files) captured across multiple product contexts.

---

## 1. Spike Overview

| Field | Entry |
|---|---|
| **Spike ID** | `SPK-010` |
| **Title** | Design & Evaluate TheoremLabs AI-Diagraming Shared Capability (TDC) |
| **Category** | `Technical / Architectural Research` |
| **Created by** | TheoremLabs Applied Innovation Labs |
| **Start Date** | 2025-10-14 |
| **Status** | Proposed |
| **Tags** | `AI-Diagraming`, `Transcripts`, `TDC`, `Tacit`, `PromptLine`, `MindMaps`, `Multi-Modal Outputs` |

---

## 2. Purpose & Hypothesis

### Purpose  
TheoremLabs is developing a family of **AI-Agent capabilities** that operate in multiple real-world settings and interaction form factors:

| Setting | Form Factor |
|----------|--------------|
| Human ↔ AI-Agent (Phone Call) | AI-Voice Agent via US/International number or Web-based Voice UX |
| Multiple Humans in Remote Meeting | AI-Meeting Assistant or AI-Notetaker integrated with MS Teams / Zoom / Google Meet |

Each AI-Agent session produces a **`.vtt` transcript**, containing one or more human voices and, in some cases, AI responses or feedback.  
This spike aims to design a **common TheoremLabs AI-Diagraming Shared Capability (TDC)** — a reusable service that can transform such transcripts (and related metadata) into **visual, audio, and knowledge artifacts**.

### Hypothesis  
> “By introducing a shared AI-Diagraming Capability, TheoremLabs can standardize how raw or processed transcripts are converted into contextual diagrams, summaries, and visual fact sheets — thereby accelerating reuse across multiple SaaS offerings (e.g., Tacit, PromptLine, ReconcileAI).”

---

## 3. Experiment / Research Method

### Objectives
1. **Survey and trial open-source or SaaS AI diagram-generation frameworks** that support API integration.  
2. **Use real `.vtt` transcripts** from Tacit or PromptLine AI sessions as test data.  
3. **Design an architecture** for a reusable TheoremLabs Diagraming Capability (TDC) that can be invoked via API, WebSocket, Webhook, or MCP Server.  
4. **Recommend candidate model(s)** or APIs for production adoption.

---

### Steps

#### Step 1 — Collect and Prepare Test Data
- Gather a set of `.vtt` transcripts from:
  - Tacit AI-Voice sessions (Human ↔ Agent)
  - PromptLine customer service or discovery calls
- Normalize metadata: speaker labels, timestamps, AI vs. human lines.
- Optionally create processed/cleaned versions of transcripts for comparison.

#### Step 2 — Research & Evaluate AI Diagramming Tools
Evaluate the following based on:
- Open-source availability and API support  
- Documentation quality and ease of embedding  
- Cost and licensing terms  
- Model accuracy and customizability  
- Supported output formats (image, video, JSON, graph)

Candidate tools to explore:
- **ErDiagramAI**, **Text2Diagram**, **DiagramGPT**, **Draw.io API**, **Mermaid.js + LLM pipelines**, **Claude/ChatGPT + Graphviz/PyGraphviz**, **Flowise or LangChain + React Flow**, etc.

#### Step 3 — Conduct Quick Technical Trials
For 2–3 selected frameworks:
- Feed raw `.vtt` transcripts directly and note results.  
- Add pre-processing (e.g., speaker attribution, keyword extraction).  
- Experiment with meta-prompts such as:
  > “Generate a mind map summarizing this customer discovery conversation.”  
  > “Draw a process flow showing customer intent, agent actions, and resolutions.”  
- Compare generated outputs for fidelity, clarity, and time-to-generate.

#### Step 4 — Define Output Typologies
| Output Type | Example |
|--------------|----------|
| 🧠 Mind Map | High-level theme visualization |
| 👥 People & Function Org Chart | Roles, departments, interaction mapping |
| 📊 Fact Sheet Diagram | Key data points / stats |
| 🔄 Process or Workflow Diagram | Customer journeys, ticket resolution steps |
| 🎧 Audio Overview (.mp3/.mp4) | Voice summary of call |
| 🎥 Video Overview (.mp4) | Animated diagram with narration |
| 🧾 Customer Ticket / Receipt (.pdf) | Structured summary of outcomes |

#### Step 5 — Architect the Shared Capability (TDC)
Define a modular design supporting multiple input & output formats.

**Input Options:**
1. Raw `.vtt` transcript  
2. Processed transcript (NER-tagged, segmented, summarized)  
3. Domain meta-prompt (e.g., “Payments Ops”, “Audit Review”)  
4. Requested Diagram Type  
5. Formatting or Styling Preferences  

**Output Options:**
- Return image URLs / base64 assets  
- Generate downloadable `.mp3` or `.mp4` summary  
- Return structured JSON descriptors for internal use

#### Step 6 — Explore Integration Options
Compare possible deployment modes:

| Option | Description | Pros | Cons |
|--------|--------------|------|------|
| **REST API Endpoint** | Standard POST `/generate-diagram` | Easy integration across apps | Stateless; less real-time |
| **WebSocket / Streaming** | Live diagram updates | Interactive UX; real-time | More complex infra |
| **Webhook** | Async callback once rendering complete | Scalable for batch jobs | Harder to debug |
| **MCP Server / Tool** | Expose as agentic protocol tool | Native to TheoremLabs MCP Ecosystem | Higher initial setup effort |

---

## 4. Tools, Data & References

| Type | Example |
|------|----------|
| **Source Data** | `.vtt` transcripts from Tacit and PromptLine |
| **Processing Tools** | Python (`webvtt`, `pandas`, `spacy`), Node.js (`vtt-to-json`) |
| **AI Diagram APIs** | DiagramGPT, OpenAI + Graphviz, Claude Sonnet + Mermaid, Flowise, Draw.io REST |
| **Visualization Libraries** | Mermaid.js, PlantUML, D3.js, React Flow |
| **Cloud Infrastructure** | AWS Bedrock, S3 (for storage), Render or Supabase for hosting |
| **References** | DiagramGPT papers, Mermaid/Draw.io docs, AWS Bedrock agents documentation |

---

## 5. Findings / Observations

*(To be completed during experimentation)*

Example notes:
- Mermaid.js integration easiest for quick prototype rendering.
- DiagramGPT API costs average $0.03–$0.05 per call with decent quality.
- Processed transcripts (entity-tagged) yield more meaningful diagram clusters.
- Adding meta-prompts like “Show workflow by speaker role” improved flow accuracy by 35%.
- Generating video/audio summaries through OpenAI’s TTS API was straightforward but expensive for large transcripts.

---

## 6. Conclusion & Recommendations

| Decision | Notes |
|-----------|--------|
| ✅ Proceed | Implement TDC as REST API first, expand to MCP Server once stable. |
| 🔁 Iterate | Run further trials on diagram layout libraries (React Flow, D3.js). |
| 🚫 Reject | Avoid closed SaaS tools with no API or license restrictions. |

**Recommendation:**  
Adopt an **open-API, model-agnostic approach** with `Mermaid.js + GPT-4o` and `Graphviz` for visual outputs.  
Integrate TDC as a **shared microservice** callable via API or MCP Server, enabling any TheoremLabs SaaS (Tacit, PromptLine, ReconcileAI, etc.) to generate AI-enhanced diagrams or summaries from transcripts.

---

## 7. Related Spikes / References

- [SPK-005: AI-Voice Agent Evaluation for PromptLine]  
- [SPK-007: Agentic Meeting Assistant for Teams/Zoom]  
- [SPK-009: SyntheticEdge Data Generation Spike]  

---

## 8. Attachments

- `/assets/` → screenshots of sample diagrams  
- `/code/` → prototype scripts to call APIs  
- `/samples/` → `.vtt` files from Tacit / PromptLine sessions  
- `/logs/` → latency & cost benchmarks  

---

## 9. TL;DR Summary

This spike designs and evaluates a **shared AI-Diagraming Service (TDC)** to convert AI-Agent conversation transcripts into mind maps, workflows, and multimedia summaries.  
Through open-source and SaaS API trials, we will determine which AI models best support diagram generation, and propose an implementation architecture (API/WebSocket/Webhook/MCP) for integration across TheoremLabs’ AI ecosystem.

---

*Notes / Tips:*
- Keep the scope focused on **architecture clarity** and **model comparability**.  
- Reuse Tacit or PromptLine transcripts for consistent benchmarks.  
- Prioritize tools that return **structured metadata** along with visual outputs.  
- Document integration latency, rendering times, and API costs clearly.




