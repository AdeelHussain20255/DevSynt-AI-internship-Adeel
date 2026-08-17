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