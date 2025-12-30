# 🧩 TheoremLabs R&D Spike — Indian Voice Infrastructure Search

> A Research Spike to **identify, evaluate, and prototype** with an India-based Voice AI platform that offers an equivalent capability set to **ElevenLabs** (Conversational AI / Voice Agent Infrastructure) but aligns with **Indian market pricing**.

---

## 1. Spike Overview

| Field | Entry |
| :--- | :--- |
| **Spike ID** | `SPK-007-Indian-Voice-Infrastructure` |
| **Title** | **Evaluation of India-Native Voice Agent Platforms** |
| **Category** | `AI Infrastructure / Vendor Selection` |
| **Start Date** | *Immediate* |
| **Status** | Proposed |
| **Tags** | `Voice Agents`, `India SaaS`, `Sarvam AI`, `Bhashini`, `Cost Optimization` |

---

## 2. Purpose & Hypothesis

### Purpose
ElevenLabs provides a seamless, high-quality Voice Agent infrastructure, but its US-centric pricing is often prohibitive for the Indian market. We require a functional **equivalent infrastructure or SaaS** hosted in India (or optimized for the region) that provides similar low-latency, conversational capabilities but is priced in **Indian Rupees (INR)** or aligned with local purchasing power.

### Hypothesis
> "Emerging India-native Voice AI platforms (e.g., Sarvam AI, Murf, or similar) offer a comparable 'Voice Agent' experience (latency <1s, natural interruptibility) to ElevenLabs at a price point significantly more viable for high-volume Indian deployments."

---

## 3. Research & Execution Method

### Key Objectives
1.  **Vendor Discovery:** Identify India-based (or India-focused) Voice AI platforms that offer **Conversational Agent APIs** (similar to ElevenLabs' Conversational AI).
2.  **Feature Parity Check:** Evaluate these platforms for critical features:
    * **Latency:** Is it usable for real-time conversation?
    * **Quality:** Do the voices sound natural and handle Indian accents/names correctly?
    * **Interruptibility:** Does the infrastructure handle user interruptions (barge-in) natively?
3.  **Integration PoC:** Build a standard "Meeting Assistant" or "Customer Support" prototype using the selected Indian platform to validate ease of integration.

### Output Typologies

| Output Type | Expectation |
| :--- | :--- |
| **Vendor Matrix** | Comparison of features: ElevenLabs vs. Indian Alternatives. |
| **PoC Codebase** | Functional prototype connected to the selected Indian SaaS. |
| **Cost Analysis** | Direct comparison of INR pricing vs. ElevenLabs USD pricing. |
| **Latency Benchmark** | Latency logs from the PoC testing. |

---

## 4. Findings / Observations

* **Vendor Capabilities:** Which platforms offer a full "Agent" endpoint versus just TTS/STT APIs?
* **Infrastructure:** Is the platform hosted in India (Mumbai/Delhi regions)?
* **Pricing Structure:** Is pricing per minute, per character, or flat rate?

---

## 5. Conclusion & Recommendations

* **Recommended Platform:** The primary choice for an Indian Voice Agent infrastructure.
* **Trade-offs:** What features (if any) are lost by moving away from ElevenLabs?
* **Implementation Guide:** Steps to integrate this platform into our current stack.

---

## 6. Attachments

* `/src/` → PoC Source Code
* `/docs/` → Vendor Pricing Sheets
* `/metrics/` → Latency Comparison Logs

---

## 7. TL;DR Summary

Find and validate an **Indian equivalent to ElevenLabs**. The goal is to secure a platform that offers **Voice Agent capabilities** with **India-based pricing**. Deliverables include a comparative analysis and a working prototype using the best local alternative.
