## 1. Spike Overview

| Field | Entry |
|---|---|
| **Spike ID** | spike-001-AG-UI|
| **Title** | Evaluate AG-UI protocol for agentic UX across frameworks |
| **Category** | `Technical / Framework Evaluation` |
| **Created by** | Prashant Sarode|
| **Start Date** | 2025-10-11 |
| **Status** | Proposed / In Progress / Completed |
| **Tags** | `AG-UI`, `Agent UI`, `Protocol`, `Interoperability` |
---


## 2. Purpose & Hypothesis

### Purpose  
AG-UI is an open, event-based protocol that standardizes how agents connect to frontends (user UIs) across frameworks. 
This spike will assess whether AG-UI is usable, performant, and flexible enough to serve as a **common UX layer** for agentic apps built with different underlying agent frameworks (LangChain, CrewAI, LlamaIndex, etc.).

### Hypothesis  
> “Using AG-UI as a middleware UX layer will reduce the custom integration effort across agent frameworks, while still delivering responsive, rich UI interactions (e.g. streaming, state sync, tool invocations).”

---

## 3. Experiment / Research Method

Here’s how we’ll test the hypothesis:

### Steps

1. **Set up minimal AG-UI demo**  
   - Use the AG-UI quickstart (e.g. `npx create-ag-ui-app`) to spin up a sample frontend.
   - Connect it to a dummy backend using their reference HTTP implementation.

2. **Integrate two agent frameworks via AG-UI**  
   - Choose **LangChain** and **CrewAI** (or LlamaIndex) as sample agent backends.  
   - Build adapters or “connectors” so each agent framework emits/responds to AG-UI events.  
   - Example: when user asks a question, send it via AG-UI input event → agent processes → return messages via AG-UI streaming / state events.

3. **Test user interaction features**  
   - Streaming responses (token-by-token)  
   - Real-time context updates (e.g. user edits, follow-up)  
   - Tool invocation (agent triggers tools or actions via UI)  
   - Multi-turn interactions, UI state sync (e.g. pending tool results, UI loading, errors)

4. **Benchmark & compare**  
   - Measure latency, event overhead, memory/CPU cost  
   - Developer effort (lines of adapter code)  
   - UX smoothness (perceived lags, stutters)  
   - Edge cases (disconnects, reconnections, partial failures)

5. **Document challenges & patching**  
   - What gaps or mismatches did you find between AG-UI and agent framework APIs?  
   - What middleware or bridging logic was required?  
   - Are there missing event types or protocol features?

---

## 4. Tools, Data & References

| Type | Example Entry |
|---|------------------|
| **SDK / Protocol** | AG-UI (TypeScript SDK, HTTP connector)  |
| **Agent Frameworks** | LangChain, CrewAI (or LlamaIndex) |
| **Frontend Stack** | React, Svelte, or Vue (whatever AG-UI sample supports) |
| **Backend / Adapter** | Node.js, Python – minimal server to translate between agent APIs and AG-UI events |
| **Test Data / Prompts** | 5–10 sample user queries, context sets |
| **Metrics Tools** | Browser devtools, Node perf counters, profiling |
| **References / Docs** | AG-UI GitHub & docs , agent framework docs, related blog posts |

---

## 5. Findings / Observations

Document what you discover. Some mock example findings:

- Connecting LangChain and CrewAI through AG-UI required ~120 lines of adapter logic per framework.  
- Streaming via AG-UI was smooth in Chrome, but had micro-pauses under slow network (< 3 Mbps).  
- The AG-UI event schema lacked a “partial update” event (e.g. editor cursor position), which we patched with a custom extension.  
- Memory overhead increased by ~15 % compared to direct framework embedding (due to protocol serialization).  
- Error reconnection logic (agent backend reconnect) caused UI flicker with current AG-UI default reconnect behavior.

Include any code snippets, screenshots, logs, or charts in `/assets/` or logs in `/notes/`.

---

## 6. Conclusion & Recommendations

| Decision | Notes |
|-----------|--------|
| ✅ Adopt | Use AG-UI as UX layer for new projects, build adapters per agent framework. |
| 🔁 Iterate | Use AG-UI for small features first (e.g. chat UI), then expand to tool integration. |
| 🚫 Reject | The overhead and adaptation complexity outweigh benefits for our use cases. |

**Recommendation:**  
Based on prototypes, AG-UI is promising as a unified UI protocol. I recommend piloting it in one internal project (LangChain + AG-UI) while continuing to refine custom connectors for others.

---

## 7. Related Spikes / References
- AG-UI GitHub & docs: https://github.com/ag-ui-protocol/ag-ui
- Quick 20min Video on AG-UI concept and quick example using Mastra Agents framework: https://youtu.be/fhF1qSyg9j4?si=vI-sQ1uLLeSu1Ar4

---

## 8. Attachments

Place any support files here:

- `/assets/` → UI screenshots, interaction diagrams  
- `/code/` → adapter modules, demo frontend/backends  
- `/logs/` → performance logs, profiling outputs  

---

## 9. TL;DR Summary

This spike evaluated **AG-UI** as a vendor-agnostic UI protocol for agentic applications. We built adapters for LangChain and CrewAI, tested streaming, state sync, and error recovery. While AG-UI accelerated UI integration across frameworks, we ran into performance overhead and minor protocol gaps (e.g. lack of “partial update” event). I recommend a pilot adoption path with iterative connector improvements.

---

*Notes / Tips:*

- Keep each spike **bounded in time** (ideally ≤ 7 days)  
- Code for **“just enough” to learn** — don’t over-engineer  
- Document **failures and gaps** — they’re just as valuable  
- Use clear naming: example folder name `spk-007-ag-ui-evaluation`

Good luck! Let me know if you’d like a companion **`submission-guide.md`** tuned for AG-UI spike submissions.
::
```
