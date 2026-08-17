# Project 1: SlotWise — AI-Powered Telegram Booking Concierge

An autonomous AI booking concierge deployed on Telegram capable of handling service appointments, enforcing strict scope boundaries, sanitizing system responses in real-time, and seamlessly routing out-of-scope requests to human support via bifurcated Google Sheets databases.

---

## 📌 Project Overview

| Feature | Technical Details |
| :--- | :--- |
| **Bot Platform** | Telegram Bot API |
| **Automation Engine** | n8n Workflow Automation |
| **AI LLM Engine** | Google Gemini API (via n8n AI Agent) |
| **Memory Management** | Window Buffer Memory / Simple Memory |
| **Backend Database** | Google Sheets (`SlotWise_Database`) |
| **Database Tabs** | `Bookings` (Confirmed) & `Handoffs` (Escalated) |
| **Public Webhook Tunnel** | ngrok Static Tunnel (`https://overact-porthole-vitally.ngrok-free.dev`) |
| **Response Sanitization** | Dynamic JavaScript Regex Tag Stripping |

---

## 🧠 System Architecture & Workflow Logic

The SlotWise architecture is designed around a single-agent bifurcated state engine:

```text
[Telegram Inbound] ──► [Telegram Trigger] ──► [AI Agent + Gemini LLM]
                                                     │
                                             (Outputs Tagged Text)
                                                     │
                                                     ▼
                                              [Switch Node]
                                            /               \
                 [BOOKING_COMPLETE] Tag   /                   \   [HANDOFF_TRIGGERED] Tag
                                         ▼                     ▼
                             [Google Sheets: Bookings]   [Google Sheets: Handoffs]
                                         \                     /
                                          \                   /
                                           ▼                 ▼
                                        [HTTP Request (Regex Clean)]
                                                     │
                                                     ▼
                                        [Telegram Outbound Reply]
```

---

## 🛠️ Key Technical Implementations

### 1. Intent Extraction & Guardrail Prompting

The AI Agent utilizes Google Gemini to parse service details (`Service Name`, `Date`, `Time`) from natural language conversations. If a user asks off-script questions (general knowledge, coding, negotiations, price disputes), the system prompt forces an immediate control tag `[HANDOFF_TRIGGERED]` to prevent AI hallucination or out-of-scope responses.

### 2. Switch Node Bifurcated Routing

Inbound AI outputs pass through an n8n **Switch Node** evaluating two condition rules:

* **Booking Route:** Matches outputs containing `[BOOKING_COMPLETE]`. Parses extracted values and appends `Username`, `Service`, `Date`, `Time`, and `Status: Confirmed` to the `Bookings` sheet.
* **Handoff Route:** Matches outputs containing `[HANDOFF_TRIGGERED]`. Appends `Username`, `User Message`, `Reason`, `Status: Pending Review`, and `Timestamp` to the `Handoffs` sheet.

### 3. Dynamic Response Sanitization

To prevent system control tags from leaking to the end-user, the final **HTTP Request** node returning messages to Telegram sanitizes the AI output dynamically:

```javascript
{{ $('AI Agent').item.json.output.replace(/\[BOOKING_COMPLETE:.*?\]|\[HANDOFF_TRIGGERED\]/g, '').trim() }}
```

---

## 📸 Proof of Work & Execution Logs

### 1. End-to-End Telegram Chat

### 2. Confirmed Bookings Database Log

### 3. Human Handoff & Escaped Queries Log

### 4. n8n Visual Canvas

### 5. Verified Execution Paths (Booking vs. Handoff)

| Booking Path Execution (#90) | Handoff Path Execution (#93) |
| --- | --- |
| | |

---

## 📁 Project Deliverables

* `workflow.json` — Sanitized n8n workflow export file.
* `assets/` — Visual proof of system architecture, live traces, and database logs.