# 🇮🇳 Spike 6: The "India-Native" Telephony Stack

> A Research Spike to **discover, validate, and prototype** a telephony infrastructure specifically optimized for the Indian market. The goal is to move away from generic US providers and find a solution that solves for **DoT Compliance**, **Call Deliverability (avoiding Spam tags)**, and **Local Pricing**.

---

## 1. Spike Overview

| Field | Entry |
| --- | --- |
| **Spike ID** | `SPK-IN-001-India-Telephony-Discovery` |
| **Title** | **Design & PoC: India-Native Twilio equivalent Infrastructure** |
| **Category** | `Infrastructure / VoIP Engineering` |
| **Start Date** | *Immediate* |
| **Status** | Proposed |
| **Tags** | `VoIP`, `SIP Trunking`, `DoT Compliance`, `DLT Registration`, `Cost Engineering` |

---

## 2. Purpose & Hypothesis

### Purpose

Our current US-based VoIP stack is not viable for India due to high costs (~$0.015/min) and poor answer rates (often flagged as spam/scam). We need to identify a **local telephony partner** or a **configured SIP architecture** that provides legitimate +91 presence, complies with local telecom regulations (TRAI/DoT), and significantly lowers per-minute costs.

### Hypothesis

> "By shifting to a region-specific telephony provider and correctly implementing DLT (Distributed Ledger Technology) protocols, we can increase call pickup rates by >30% while reducing operational costs by >50% compared to standard US carriers."

---

## 3. Experiment / Research Method

### Objectives

1. **Market Discovery:** Identify at least 3 viable telephony providers that offer programmatic voice (API/SIP) with strong infrastructure in India.
2. **Compliance Mapping:** Document the exact "Happy Path" to getting a legitimate business phone number in India. What is the DLT registration? What KYC documents are hard blockers?
3. **Prototype Build:** Select the most promising provider and build a functional "Hello World" calling application.

### Steps

#### Step 1 — Vendor Evaluation

* Research providers based on:
* **Cost:** Price per minute for outbound calls to +91 mobile numbers.
* **Connectivity:** Direct carrier connections vs. aggregators (affects latency).
* **Features:** Support for WebSockets/Media Streams (critical for AI agents).



#### Step 2 — The Compliance "Paper Chase"

* Investigate the requirements for:
* Obtaining a local +91 Mobile or Landline number.
* Registering a "Sender ID" / Business Name to avoid Spam filters (Truecaller/Carrier databases).
* *Note: If actual verification takes weeks, document the process and use a sandbox/unverified number for the PoC.*



#### Step 3 — Technical PoC

* Write a script (Python/Node.js) that:
* Initiates an outbound call to your personal Indian mobile number.
* Plays a static audio file or TTS message upon answer.
* Logs the "Post-Dial Delay" (time between API request and phone ringing).



#### Step 4 — Output Typologies

| Output Type | Expectation |
| --- | --- |
| **Vendor Matrix** | Comparison table of 3 vendors (Cost, Features, API limitations). |
| **Compliance Guide** | A "How-To" generic guide for onboarding a US company to Indian Telecom. |
| **PoC Code** | Functional repository triggering a call. |

#### Step 5 — Implementation Outline (PoC)

* **Inputs:** Destination Number (+91...), Auth Credentials.
* **Process:** API Trigger  Carrier Routing  Handset Ring  Audio Playback.
* **Success Metric:** The phone rings within 5 seconds, and the audio is clear.

---

## 4. Tools, Data & References

| Type | Tool/Reference |
| --- | --- |
| **Search Queries** | "Cloud Telephony Providers India", "Programmatic Voice API India", "TRAI DLT Registration for Voice" |
| **Testing** | Personal Mobile Device (Jio/Airtel/Vi networks for diverse testing) |
| **Verification** | Truecaller App (to check how the number appears to users) |

---

## 5. Findings / Observations

*(To be filled by Candidate)*

* **Vendor Choice:** Why did you choose Vendor X over Vendor Y?
* **Cost Discovery:** What is the actual price per minute (INR)? Are there hidden platform fees?
* **Latency:** Did you observe significant lag? Was it carrier-dependent?

---

## 6. Conclusion & Recommendations

*(To be filled by Candidate)*

* **Recommendation:** Which provider should we contract with?
* **Architecture:** Should we use SIP trunking or a high-level API?
* **Next Steps:** What is required to move this PoC to production?

---

## 7. Deliverables Checklist

* [ ] **Vendor Comparison Matrix:** (Excel/Markdown table)
* [ ] **Compliance "Cheat Sheet":** (PDF/Markdown)
* [ ] **Source Code Repository:** (GitHub link)
* [ ] **Cost Analysis Model:** (Spreadsheet projecting 10k minutes/month)

---
