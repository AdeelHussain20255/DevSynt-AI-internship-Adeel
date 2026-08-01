# DevSynt AI Automation Internship — Summer 2026

Welcome to the repository for my **AI Automation Internship** at **DevSynt**. This repository tracks my ongoing progress, workflow automation projects, and task deliverables throughout the program.

---

## 📌 Internship Information

| Field | Details |
| :--- | :--- |
| **Intern** | Adeel Hussain |
| **Track** | AI Automation |
| **Mentor** | Afnan Shoukat |
| **Repository** | `devsynt-ai-internship-adeel` |

---



## 🚀 Task 1: Local n8n Setup & Public Webhook Exposure

### Overview
Successfully configured a local **n8n** workflow automation environment, exposed it to the public internet via a persistent static **ngrok** reverse-proxy tunnel, and initialized this repository to track all internship deliverables.

---

### ⚙️ Environment Configuration

* **Local Instance:** `http://localhost:5678`
* **Public Domain:** `https://overact-porthole-vitally.ngrok-free.dev`
* **Runtime:** Node.js & npm

---

### 🛠️ Implementation Steps

#### 1. Local n8n Server Setup
Installed n8n globally using `npm` and initialized the local server instance on the default port (`5678`):

```bash
# Install n8n globally
npm install n8n -g

# Start the n8n instance
n8n start
```

> **Verification:** Verified local web UI accessibility by visiting `http://localhost:5678`.

#### 2. Static ngrok Tunnel Configuration
To allow external webhooks to hit the local n8n instance seamlessly without changing endpoints on restart:
1. Claimed a persistent static domain via the ngrok dashboard: `overact-porthole-vitally.ngrok-free.dev`.
2. Authenticated the local ngrok CLI.
3. Established a secure reverse-proxy tunnel targeting port `5678`:

```bash
ngrok http 5678 --url=overact-porthole-vitally.ngrok-free.dev
```
![ngrok Reverse Proxy Tunnel Active](assets/ngrok.png)

#### 3. Account Initialization & Verification
* Navigated to `https://overact-porthole-vitally.ngrok-free.dev` in the browser to confirm public routing.
* Completed the primary owner account registration (email, profile setup, and security credentials).
* Verified full access and execution functionality on the n8n visual workflow canvas.

![n8n Editor Access via Public Domain](assets/n8n.png)
---


---

## 🚀 Task 2: WhatsApp Lead-to-Booking System (Phase 1)

### Overview
Designed and deployed Phase 1 of an automated **WhatsApp Lead-to-Booking pipeline** tailored for **Apex Dental Care**. This phase establishes a live, two-way communication bridge between Meta's WhatsApp Cloud API Sandbox and a local **n8n** automation engine exposed publicly via an **ngrok** tunnel. The system dynamically receives incoming user messages (supporting English and Urdu conversational workflows) and dispatches automated responses back through Meta's Graph API.

---

### ⚙️ System Architecture & Parameters

| Parameter | Configuration |
| :--- | :--- |
| **Niche / Business** | Apex Dental Care |
| **Primary Language** | Urdu / English (Bilingual Support) |
| **Messaging Platform** | Meta WhatsApp Cloud API (Sandbox Mode) |
| **Webhook Tunnel** | `https://overact-porthole-vitally.ngrok-free.dev/webhook/whatsapp` |
| **Automation Engine** | n8n Workflow Automation |
| **API Version** | Meta Graph API `v20.0` |

---

### 🛠️ Key Implementation Steps

#### 1. Webhook Handshake & Verification (`GET`)
* Configured an initial `Webhook` and `Respond to Webhook` node pairing in n8n to process Meta’s initial validation request (`hub.challenge`).
* Verified the webhook token securely against Meta's Developer Console to activate live event subscriptions.

#### 2. Inbound Message Ingestion (`POST`)
* Set up a dedicated POST webhook listener in n8n to ingest real-time JSON payloads containing inbound sender phone numbers (`wa_id`) and text content.

#### 3. Outbound Graph API Response Node
* Configured an **HTTP Request** node targeting Meta's messaging endpoint:
  `POST https://graph.facebook.com/v20.0/{PHONE_NUMBER_ID}/messages`
* Authenticated calls using Bearer Tokens and structured JSON payloads to deliver instant dynamic auto-replies back to WhatsApp users.

#### 4. Modular Configuration
* Externalized core bot settings, business info, system prompts, and state values into a modular `config.json` file for scalable future expansion.

---

### 📸 Execution Proof & Verification

#### 1. Visual Workflow Architecture
*Full node graph processing incoming webhooks and dispatching Meta Graph API POST requests.*
![n8n Workflow Canvas](assets/n8n-workflow-canvas.jpeg)

#### 2. Successful Execution Log
*Green success status (`200 OK`) in n8n confirming valid payload receipt and API response dispatch.*
![n8n Webhook Execution Success](assets/webhook-test-screenshot.jpeg)

#### 3. Active Tunnel Monitoring
*Active ngrok reverse proxy handling live webhook traffic with HTTP 200 response codes.*
![ngrok Tunnel Status](assets/ngrok-tunnel-status.jpeg)

#### 4. End-to-End WhatsApp Chat Test
*Live WhatsApp test conversation confirming incoming user prompts and automated n8n responses.*
![WhatsApp Chat Proof](assets/whatsapp-reply-test.jpeg)


## 📁 Repository Structure

```text
.
├── assets/      # Screenshots & visual proof of work
│   ├── n8n.png
│   └── ngrok.png
├── README.md
└── tasks/       # Upcoming automation workflows & export files
