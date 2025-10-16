# 🎙️ TheoremLabs R&D Spike — Meeting Voice Agent (MVA)

> A Research Spike to explore, evaluate, and validate a **meeting voice agent** that joins **Zoom or Google Meet** via audio, converses with a human in real time (preferably **ElevenLabs**-based), and **stores both transcript and audio** after the session.

---

## 1. Spike Overview

| Field          | Entry                                                                                               |
| -------------- | --------------------------------------------------------------------------------------------------- |
| **Spike ID**   | `SPK-004-Theorem-Meeting-Voice-Agent`                                                               |
| **Title**      | Design & Evaluate Meeting Voice Agent (MVA) for Zoom/Google Meet                                    |
| **Category**   | `Technical / Architectural Research`                                                                |
| **Created by** | TheoremLabs Applied Innovation Labs                                                                 |
| **Start Date** | 2025-10-16                                                                                          |
| **Status**     | Proposed                                                                                            |
| **Tags**       | `Zoom`, `Google Meet`, `Voice Agent`, `ElevenLabs`, `Transcripts`, `Audio Recording`, `PoC`, `Cost` |

---

## 2. Purpose & Hypothesis

### Purpose

Enable TheoremLabs to deploy a **minimal voice agent** that can **join Zoom or Google Meet via audio**, conduct a **two-way conversation** during the meeting, and **persist the transcript and audio** artifacts. This spike focuses on a **working PoC** using a simple LLM-backed agent (preferably **ElevenLabs**), prioritizing feasibility, implementation path, and cost visibility.

### Hypothesis

> “By leveraging meeting dial-in options and a provider that supports real-time media to an LLM-powered voice runtime, TheoremLabs can deliver a practical PoC with acceptable latency and clear post-call artifacts (audio + transcript) at predictable cost.”

---

## 3. Experiment / Research Method

### Objectives

1. **Verify feasibility** of joining Zoom/Google Meet via available audio entrypoints.
2. **Demonstrate a working PoC** that conducts a short interactive conversation.
3. **Store meeting artifacts**: full-session audio and machine-generated transcript.
4. **Document implementation path** with clear inputs/outputs and operational steps.
5. **Estimate cost** for typical sessions (per minute, per meeting).

---

### Steps

#### Step 1 — Collect and Prepare Test Data

* Define **test meetings** (one Zoom, one Google Meet) with access details.
* Prepare a **short conversation script** (greetings, Q&A, closing) to standardize trials.
* Establish **evaluation checklists** (latency, intelligibility, turn-taking quality).

#### Step 2 — Research & Evaluate Meeting Entry Options

Evaluate meeting audio entry methods for PoC suitability:

* **Dial-in (PSTN) access** to Zoom/Meet.
* **SIP interop** (if available on the account).
* **Any provider-supported audio bridge** suitable for real-time agent interaction.

Comparison criteria:

* Availability and ease of setup
* Call stability and latency
* Requirements (licenses, account tiers)
* Recording/transcript permissibility and compliance

#### Step 3 — Conduct Quick Technical Trials

Run **two short trials** (e.g., 5–10 minutes each):

* **Trial A (Zoom)**: Join, converse, end; capture artifacts.
* **Trial B (Google Meet)**: Join, converse, end; capture artifacts.

For each trial, record:

* Join success and time-to-join
* Conversational turn-taking quality
* Post-call artifact availability (audio + transcript)

#### Step 4 — Define Output Typologies

| Output Type                | Example                                              |
| -------------------------- | ---------------------------------------------------- |
| 🧾 **Transcript**          | Timestamped text with speaker tags (agent/human)     |
| 🔊 **Audio Recording**     | Full-session audio file or segments                  |
| 📑 **Session Summary**     | Key points, action items, outcome                    |
| 📊 **Operational Metrics** | Join success, duration, latency notes, cost snapshot |

#### Step 5 — Implementation Outline (PoC)

Inputs:

1. **Meeting access info** (service, dial-in or interop method, credentials).
2. **Agent selection** (LLM model, voice profile, basic system prompt).
3. **Recording & transcript flags** (enabled/disabled, retention period).

Outputs:

* **Audio file(s)** for the session.
* **Transcript file** (JSON or text with timestamps).
* **Minimal session metadata** (start/end, duration, identifiers).

Operational notes:

* Keep **turn-taking brief** to reduce latency impact.
* Apply **basic PII controls** (redaction policy, retention setting).
* Store artifacts in a **versioned bucket** with predictable paths.

#### Step 6 — Feasibility, Implementation & Cost Reporting

* **Feasibility**: Summarize which entry methods worked and under what conditions.
* **Implementation**: List the exact configuration steps used for the successful PoC path.
* **Cost**: Provide a simple per-minute and per-session estimate (see Section 5/6).

---

## 4. Tools, Data & References

| Type                     | Example                                                                         |
| ------------------------ | ------------------------------------------------------------------------------- |
| **Meeting Platforms**    | Zoom, Google Meet                                                               |
| **Voice Agent Runtime**  | ElevenLabs Conversational AI (preferred) or comparable LLM-backed voice agent   |
| **Processing Utilities** | Basic diarization/speaker tagging (optional), timestamped transcript formatting |
| **Storage**              | Object storage for audio + transcript + metadata                                |
| **Compliance**           | Meeting owner consent, recording notifications, retention policy                |

---

## 5. Findings / Observations

*(To be completed during experimentation)*

Example notes:

* **Entry Method**: Dial-in worked reliably for both platforms with minimal setup.
* **Conversation Quality**: Short turns improved perceived responsiveness.
* **Artifacts**: Audio and transcript consistently saved; timestamps aligned within ±1s.
* **Limitations**: Lobby/passcode prompts require predictable flows; longer sessions increase storage noticeably.

---

## 6. Conclusion & Recommendations

| Decision      | Notes                                                                            |
| ------------- | -------------------------------------------------------------------------------- |
| ✅ Proceed     | Adopt the **working PoC path** (documented in Step 6) for initial pilots.        |
| 🔁 Iterate    | Explore alternative entry methods to reduce latency and improve audio quality.   |
| 📈 Scale      | Add summary generation, diarization, and structured action-item extraction.      |
| 🔒 Compliance | Enforce recording consent banners and configurable retention (e.g., 30–90 days). |

**Recommendation:**
Advance with the **validated PoC** route, maintain a **provider-agnostic** stance for meeting entry, and formalize **artifact storage & cost tracking** before wider rollout.

---

## 7. Related Spikes / References

* [SPK-003: WhatsApp Calling & Messaging Agent (WCA)]
* [SPK-005: AI-Voice Agent Evaluation for PromptLine]
* [SPK-007: Agentic Meeting Assistant for Teams/Zoom]

---

## 8. Attachments

* `/assets/` → screenshots of meeting test runs (redacted)
* `/samples/` → example transcript snippets (redacted)
* `/logs/` → join/leave timestamps, latency notes, per-run metrics
* `/costs/` → per-minute and per-session cost worksheets (inputs and outputs)

---

## 9. TL;DR Summary

This spike validates a **meeting voice agent** that **joins Zoom/Google Meet**, **converses via audio**, and **stores transcript + audio**. The focus is a **working PoC**, a **clear implementation outline**, and a **simple, transparent cost model** to inform next steps.

---

*Notes / Tips:*

* Keep initial conversations **short and structured** to evaluate latency and turn-taking.
* Use **consistent meeting settings** to reduce variability in join flows.
* Start with **conservative retention** and **redaction**; revise with stakeholders after the PoC.
