# 📞 TheoremLabs R&D Spike — WhatsApp Calling & Messaging Agent (WCA)

> Research spike to evaluate and prototype **WhatsApp Calling + Messaging** for TheoremLabs agents (with a preference for an **ElevenLabs voice agent**), validating feasibility via **Twilio**, **Meta’s WhatsApp Cloud API**, and **other SaaS/providers** that expose compliant WhatsApp calling/messaging interfaces.

---

## 1. Spike Overview

| Field          | Entry                                                                                                 |
| -------------- | ----------------------------------------------------------------------------------------------------- |
| **Spike ID**   | `SPK-003-Theorem-WhatsApp-Calling-Agent`                                                              |
| **Title**      | WhatsApp Calling & Messaging Agent (WCA) — Feasibility, Trials & Architecture                         |
| **Category**   | `Technical / Architectural Research`                                                                  |
| **Created by** | TheoremLabs Applied Innovation Labs                                                                   |
| **Start Date** | 2025-10-15                                                                                            |
| **Status**     | Proposed                                                                                              |
| **Tags**       | `WhatsApp`, `Calling`, `Messaging`, `ElevenLabs`, `Twilio`, `Voice-Agent`, `MCP`, `Provider-Agnostic` |

---

## 2. Purpose & Hypothesis

### Purpose

Evaluate whether we can offer a **single WhatsApp entrypoint** for both **messaging** and **real-time voice calls** that routes to a **voice AI agent** (preferably ElevenLabs Conversational AI), and ship a minimal prototype that can:

* **Receive user-initiated WhatsApp calls** and route audio to an AI agent.
* **Initiate business-initiated calls** (where permitted) from an existing WhatsApp message thread.
* **Handle WhatsApp messaging** (templates, session messages) in the same thread for follow-ups and automation.

We will compare three integration paths:

1. **Twilio** (WhatsApp + voice media bridge),
2. **Meta WhatsApp Cloud API** (direct),
3. **Other SaaS/providers** (provider-agnostic discovery; do not preselect—evaluate any that meet requirements).

### Hypothesis

> “By unifying WhatsApp messaging and calling and bridging call media to an ElevenLabs agent, TheoremLabs can create a low-friction, global entrypoint that improves contact rates and reduces onboarding friction compared to traditional phone IVRs.”

---

## 3. Experiment / Research Method

### Objectives

1. **Confirm channel feasibility & rules**: calling availability, messaging templates/windows, user permissions.
2. **Prototype a minimal WhatsApp voice agent** using **ElevenLabs** voice runtime + one of: **Twilio**, **Meta Cloud API**, or an **alternative provider** discovered during research.
3. **Compare integration paths** on media handling, onboarding effort, cost, reliability, compliance, and observability.
4. **Document an architecture** that can be invoked via **REST**, **Webhook**, **WebSocket/Streaming**, or **MCP Tool/Server**.

---

### Steps

#### Step 1 — Test Data & Accounts

* Set up a **test WhatsApp Business Account (WABA)** with a test number or sandbox number as available from each provider.
* Prepare **sample user journeys**: inbound call → triage → agent; message → permission prompt → outbound call; post-call summary.
* Draft **messaging templates**: onboarding, opt-in confirmations, call-permission prompts, post-call summary.

#### Step 2 — Evaluate Integration Paths

**A. Twilio Path**

* Enable **WhatsApp Messaging** and **WhatsApp Calling** features.
* Use Twilio’s inbound call webhook to route WhatsApp VoIP calls into **Twilio Voice** and connect a **Media Stream/WebRTC** to our **ElevenLabs agent**.
* Validate call control (answer, hangup), dual channel (voice + thread messages), and template usage.

**B. Meta WhatsApp Cloud API (Direct)**

* Register WABA, enable **Calling** in Cloud API, implement required **webhooks** and **call control** endpoints.
* Investigate audio/media transport to the agent (direct WebRTC/SIP/stream). If not feasible, document limitation and compare with Twilio or other providers.

**C. Other SaaS/Providers (Open Discovery)**

* Research any **WhatsApp-compliant providers** that expose calling + messaging and **media bridge/hooks** suitable for an ElevenLabs agent.
* Validate: onboarding time, pricing, support for inbound/outbound calling, media formats, webhooks, and observability.
* Do **not** restrict to a fixed short list—include any providers that meet requirements.

#### Step 3 — Quick Technical Trials (build 2–3)

* **Trial 1 (Twilio)**: WhatsApp inbound call → Twilio Voice → Media Stream → ElevenLabs agent → reply audio to caller.
* **Trial 2 (Meta Cloud API)**: Incoming call → webhook → media path to agent (or record/document constraint).
* **Trial 3 (Other Provider)**: Enable calling → confirm inbound/outbound support → attempt media relay to ElevenLabs via webhook/WebSocket/SIP; record results.

#### Step 4 — Define Output Typologies

| Output Type            | Example                                                |
| ---------------------- | ------------------------------------------------------ |
| 📞 Voice Agent Flow    | IVR-style or NLU-style triage within WhatsApp call     |
| 💬 Messaging Templates | Opt-in, call permission, follow-up summary             |
| 🧾 Post-call Summary   | WhatsApp text transcript/summary + links               |
| 📊 Ops Metrics         | Answer rate, call duration, drop rate, ASR latency     |
| 🔗 Deep Links          | “Call us on WhatsApp” and “Continue in WhatsApp” links |

#### Step 5 — Architect the Shared Capability (WCA)

**Inputs:**

* WhatsApp events (message, call started/ended), contact metadata, template IDs, **call-permission state**, agent config (ElevenLabs model/voice/tools), business context.

**Outputs:**

* **Real-time audio** to/from agent, **message replies** (text/media/templates), call control actions, **structured JSON logs** (quality, latency, costs).

**Core Components (suggested):**

* **Ingress**: Provider webhooks (messages, calls), verification.
* **Session & Policy**: Contact state, template windows, call permission gating.
* **Media Bridge**: WebRTC/SIP/stream adapter → **ElevenLabs ConvAI** (bi-directional).
* **Agent Layer**: ElevenLabs session + tools (CRM lookup, scheduler, etc.).
* **Observability**: Metrics, traces, cost accounting, transcripts.
* **Storage**: Call/message logs, template usage, opt-ins.

#### Step 6 — Integration Modes

| Option                    | Description                                                 | Pros                                 | Cons                         |
| ------------------------- | ----------------------------------------------------------- | ------------------------------------ | ---------------------------- |
| **REST API**              | `/wa/call-webhook`, `/wa/message-webhook`, `/agent/session` | Simple; fits webhook-first providers | Not streaming                |
| **WebSocket / Streaming** | Media in/out to agent                                       | Low latency; natural turn-taking     | Infra complexity             |
| **Webhook**               | Provider→WCA events                                         | Scales; clear audit logs             | Async media may be limited   |
| **MCP Tool/Server**       | Expose “wa_call”, “wa_send_template”, “wa_summary”          | Reusable inside LLM agents           | Requires MCP ops familiarity |

---

## 4. Tools, Data & References

| Type                | Example                                                                                                                           |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Providers**       | **Twilio WhatsApp + Voice**, **Meta WhatsApp Cloud API**, **Other SaaS/providers** discovered during research (do not pre-limit). |
| **Voice Agent**     | **ElevenLabs Conversational AI** (real-time agent + TTS/ASR).                                                                     |
| **Processing/Glue** | Node.js or Python for webhooks, media relay, and agent session mgmt.                                                              |
| **Infra**           | Render/Supabase/AWS/GCP for hosting; S3/Supabase for storage; Prometheus/Grafana or provider dashboards for metrics.              |
| **Compliance**      | Template rules, opt-ins, country calling restrictions, rate limits, and audit logging.                                            |

---

## 5. Findings / Observations *(to be filled during trials)*

*Example notes template:*

* **Channel Feasibility:** Calling + messaging work in provider X; provider Y supports messaging only.
* **Media Bridge:** Latency with provider X (p50, p95); codec negotiation notes; echo/AGC behavior.
* **Permissions/Windows:** Business-initiated call rules; template windows and costs.
* **Costs:** Compare setup fees, per-call/minute rates, and per-template costs; summarize break-even vs PSTN.
* **Client Requirements:** Minimum WhatsApp client version for calling; behavior on older devices.

---

## 6. Conclusion & Recommendations

| Decision                            | Notes                                                                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| ✅ Proceed (Twilio-first POC)        | Fastest bridge to an **ElevenLabs** agent; well-known media streaming patterns.                                            |
| 🔁 Explore (Meta Direct)            | Map Cloud API calling media path; if constrained, document and keep as future lane.                                        |
| 🔎 Open Discovery (Other Providers) | Continue evaluating **any** compliant WhatsApp provider with viable media hooks; do not preselect or restrict to examples. |
| ⚠️ Compliance                       | Enforce template rules, opt-ins, country restrictions; log permissions and message/call audits.                            |

**Recommendation:**
Deliver a **Twilio-first prototype** to validate WhatsApp **inbound call** → **ElevenLabs agent** quickly. In parallel, **research and trial other providers** (no preselection) and **Meta Cloud API** direct calling; choose long-term path based on latency, reliability, cost, and compliance ergonomics.

---

## 7. Related Spikes / References

* [SPK-005: AI-Voice Agent Evaluation for PromptLine]
* [SPK-007: Agentic Meeting Assistant for Teams/Zoom]
* [SPK-009: SyntheticEdge Data Generation Spike]

---

## 8. Attachments

* `/assets/` → call flow diagrams, latency charts
* `/code/` → example webhook + media bridge to ElevenLabs
* `/samples/` → template JSON (opt-in, call-permission)
* `/logs/` → call success/fail, permission outcomes, cost snapshots

---

## 9. TL;DR Summary

Prototype a **WhatsApp Calling + Messaging** entrypoint that routes **voice calls** to an **ElevenLabs agent**, comparing **Twilio**, **Meta Cloud API**, and **any other viable providers**. Start with a Twilio-based POC, keep **provider-agnostic** options open, and select the long-term path based on performance, cost, and compliance.

---

### Appendix A — Minimum POC Checklists

**Twilio Path**

* [ ] Enable WhatsApp number + Calling
* [ ] Webhook: `/wa/call-webhook`
* [ ] Media Stream/WebRTC bridge → ElevenLabs agent
* [ ] Messaging templates (opt-in / post-call summary)
* [ ] Metrics: answer %, avg duration, ASR latency, cost per call

**Meta Cloud API Path**

* [ ] WABA registration; enable Calling
* [ ] Webhooks for call events + messaging
* [ ] Media transport to agent (WebRTC/SIP/stream) or document limitation
* [ ] Permission + compliance flows

**Other Provider Path (Open Discovery)**

* [ ] Evaluate onboarding time, pricing, inbound/outbound support
* [ ] Confirm media relay to ElevenLabs (webhook/WebSocket/SIP)
* [ ] Verify observability & export of transcripts/metrics
* [ ] Record gaps/risks and recommended mitigations

---

### Notes / Tips

* Keep **agent turn-taking** smooth with low-latency streaming.
* Track **template windows & permissions** carefully.
* Prefer providers with **structured events + media hooks**; avoid lock-in by designing a pluggable **provider adapter** layer.
