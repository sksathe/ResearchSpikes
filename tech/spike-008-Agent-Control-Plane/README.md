# 💻 TheoremLabs R&D Spike — The Agent Control Plane

## 1. Spike Overview

| Field | Entry |
| :--- | :--- |
| **Spike ID** | `SPK-008-Agent-Control-Plane` |
| **Title** | **Secure Web App for ElevenLabs Agent & Phone Number Management** |
| **Category** | `Full-Stack Web Dev / API Integration` |
| **Created by** | TheoremLabs Applied Innovation Labs |
| **Start Date** | *Immediate* |
| **Status** | Proposed |
| **Tags** | `Next.js`, `Fastify`, `ElevenLabs API`, `Agent CRUD`, `Number Assignment` |

---

## 2. Purpose & Hypothesis

### Purpose
We need a unified "Control Plane" to manage the complete lifecycle of our voice infrastructure using **only** the ElevenLabs ecosystem. This app must serve two critical functions:
1.  **Agent Management:** Create, configure, and delete AI agents (defining their Voice ID, prompting, and settings).
2.  **Phone Number Management:** Import existing Twilio numbers into the ElevenLabs account (via 11Labs API) and programmatically **assign, reassign, or remove** them from specific agents.

This spike validates a decoupled architecture (Next.js + Fastify) to securely wrap these native 11Labs capabilities into a single dashboard.

### Hypothesis
> “By wrapping the ElevenLabs Agent APIs (`/v1/convai/agents`) and Phone Number APIs (`/v1/convai/phone-numbers`) in a secure Fastify proxy, we can build a cohesive dashboard where admins can spawn/remove agents and instantly 'hot-swap' imported numbers between them without leaving the interface.”

---

## 3. Experiment / Research Method

Here’s how we’ll test the hypothesis:

### Steps

1. **Set up Fastify Proxy Server**
   - Initialize a secure Fastify server with `@fastify/cors` and `@fastify/jwt`.
   - **Implement Agent Routes:**
     - `POST /agents`: Create new agent.
     - `GET /agents`: List all agents.
     - `DELETE /agents/:id`: Delete agent.
   - **Implement Number Management Routes (11Labs Native):**
     - `GET /numbers`: List all numbers currently imported in the ElevenLabs account.
     - `POST /numbers/import`: Proxy to `POST /v1/convai/phone-numbers/create` (accepts Twilio SID/Token to import the number *into* 11Labs).
     - `PATCH /numbers/:id/assign`: Proxy to `PATCH /v1/convai/phone-numbers/{phone_number_id}` to update the `agent_id`.
     - `DELETE /numbers/:id`: Remove a number from the 11Labs account.

2. **Build Next.js Dashboard UI**
   - **Agent View:** A grid displaying active agents with "Edit" and "Delete" actions.
   - **Number Manager View:**
     - *Import Form:* A UI to input Twilio credentials (SID/Token/Number) to trigger the import.
     - *Assignment Matrix:* A list of numbers showing their current Agent binding.
   - **Binding Action:** A dropdown UI to select an imported number and assign it to a specific agent (or reassign it).

3. **Test Integrated Lifecycle**
   - **Create:** Generate a new agent named "Support Bot".
   - **Import:** Use the UI to import a Twilio number into ElevenLabs.
   - **Assign:** Link the imported number to "Support Bot" via the dashboard.
   - **Reassign:** Create "Sales Bot", use the dashboard to switch the number from "Support" to "Sales".
   - **Verify:** Confirm via the ElevenLabs console that the `agent_id` for that phone number has updated.

4. **Benchmark & Compare**
   - Measure the latency of the "Import" operation via API.
   - Validate error handling: What happens if you try to assign a number that is currently in use without detaching it first?

5. **Document Challenges & Patching**
   - Did the 11Labs API allow "hot-swapping" (overwriting the agent ID) or did it require a two-step "Detach -> Attach" flow?
   - How does the API handle validation errors (e.g., invalid Twilio credentials during import)?

---

## 4. Tools, Data & References

| Type | Example Entry |
| :--- | :--- |
| **SDK / Framework** | Next.js (React), Fastify (Node.js backend) |
| **API Provider** | ElevenLabs Conversational AI API |
| **References / Docs** | [11Labs: Get Phone Numbers](https://elevenlabs.io/docs/api-reference/phone-numbers/get-phone-numbers), [11Labs: Add Number](https://elevenlabs.io/docs/api-reference/phone-numbers/create-phone-number) |

---

## 5. Findings / Observations

Document what you discover. Some mock example findings:

- **Assignment Logic:** The ElevenLabs API endpoint `/v1/convai/phone-numbers/{id}` accepts an `agent_id` in the PATCH body, effectively allowing hot-swapping in one request.
- **Import Validation:** The Import API returns a success message immediately, but the number takes ~5 seconds to appear in the `GET /numbers` list.
- **Dependency:** Deleting an agent does *not* automatically release the number; the number remains "assigned" to a null ID in the dashboard view, requiring a UI fix.
- **Security:** We successfully kept the Twilio credentials server-side in Fastify during the `POST /numbers/import` call, preventing client-side exposure.

Include any code snippets, screenshots, logs, or charts in `/assets/` or logs in `/notes/`.

---

## 6. Conclusion & Recommendations

| Decision | Notes |
| :--- | :--- |
| ✅ Adopt | The 11Labs API provides sufficient control for number management without needing external integrations. |
| 🔁 Iterate | Add a "Sync" button to the dashboard to refresh the number list if an import takes time to propagate. |
| 🚫 Reject | N/A |

**Recommendation:**
Proceed with this architecture. Ensure the Fastify layer validates that an Agent exists before attempting to assign a number to it to prevent API errors.

---

## 7. Related Spikes / References
- [SPK-009: Hybrid Knowledge Strategy] (Defining what these agents know)
- [SPK-006: Regional Infrastructure Benchmark] (Source of the numbers being imported)

---

## 8. Attachments

Place any support files here:

- `/backend/` → Fastify source code (Routes for Agents & 11Labs Numbers)
- `/frontend/` → Next.js source code (Dashboard Components)
- `/assets/` → UI Wireframes for the "Import Number" modal
- `/logs/` → API transaction logs

---

## 9. TL;DR Summary

This spike built a **Control Plane** using **Next.js** and **Fastify** that manages the full lifecycle of agents and phone numbers using **only ElevenLabs APIs**. We validated that admins can **Import** numbers (providing credentials to 11Labs) and **Assign/Reassign** those numbers to agents programmatically. The Fastify proxy layer secured the interactions and provided a clean API surface for the frontend dashboard.

---

*Notes / Tips:*

- Keep each spike **bounded in time** (ideally ≤ 7 days)
- Code for **“just enough” to learn** — don’t over-engineer
- Document **failures and gaps** — they’re just as valuable
- Use clear naming: example folder name `spk-008-Control-Plane`

Good luck!
contact author of this spike: research@theoremlabs.io
