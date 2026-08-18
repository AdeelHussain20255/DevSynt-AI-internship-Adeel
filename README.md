# DevSynt AI Automation Internship — Summer 2026

Hi there! Welcome to my official repository for the **DevSynt AI Automation Internship**. This space tracks my hands-on progress, system architectures, exported workflows, and documentation for every task throughout the program.

---

## 📌 Internship Overview

| Field | Details |
| :--- | :--- |
| **Intern** | Adeel Hussain |
| **Track** | AI Automation |
| **Mentor** | Afnan Shoukat |
| **Repository** | `DevSynt-AI-internship-Adeel` |

---

## 🚀 Task 1: Local n8n Setup & Public Webhook Exposure

### Overview
Before building complex automation pipelines, I needed a local environment capable of receiving real-time webhooks from external platforms like Meta. Since local servers (`localhost:5678`) can't be reached directly by public services, I configured a local **n8n** instance and connected it to a static **ngrok** reverse-proxy tunnel.

Think of webhooks like a digital mailbox—whenever an event happens online (like someone sending a WhatsApp message), WhatsApp needs an unchanging public address to "mail" that data to.

---

### ⚙️ Environment Specs

* **Local Instance:** `http://localhost:5678`
* **Static Public Tunnel:** `https://overact-porthole-vitally.ngrok-free.dev`
* **Runtime Environment:** Node.js & npm

---

### 🛠️ Step-by-Step Implementation

#### 1. Installing and Launching n8n
I installed n8n globally on my local machine using `npm` and launched the server on port `5678`:

```bash
# Install n8n globally
npm install n8n -g

# Start local server
n8n start
```

> **Check:** Opened `http://localhost:5678` in my browser to confirm the n8n editor UI was up and running locally.

#### 2. Locking in a Static ngrok Tunnel
To prevent my webhook URL from breaking every time I restarted my terminal, I reserved a permanent static domain on the ngrok dashboard and authenticated my local CLI:

```bash
ngrok http 5678 --url=overact-porthole-vitally.ngrok-free.dev
```

This established a secure, persistent bridge routing public traffic straight to port `5678` on my computer.

![ngrok Reverse Proxy Tunnel Active](assets/ngrok.png)

#### 3. Public Verification & Account Setup
* Tested public routing by opening `https://overact-porthole-vitally.ngrok-free.dev` in my browser.
* Registered my primary admin account and verified full access to the n8n visual canvas.

![n8n Editor Access via Public Domain](assets/n8n.png)

---


## 📁 Repository Structure

```text
.
├── assets/                  # Central repository for visual proofs & screenshots
│   ├── .gitkeep
│   ├── n8n-workflow-canvas.jpeg
│   ├── n8n.png
│   ├── ngrok-tunnel-status.jpeg
│   ├── ngrok.png
│   ├── webhook-test-screenshot.jpeg
│   └── whatsapp-reply-test.jpeg
├── project1/                # Project 1: SlotWise Telegram Concierge
│   ├── assets/
│   │   ├── n8n-canvas.jpeg
│   │   ├── n8n-execution-booking.jpeg
│   │   ├── n8n-execution-handoff.jpeg
│   │   ├── sheets-bookings.jpeg
│   │   ├── sheets-handoffs.jpeg
│   │   └── telegram-chat.jpeg
│   ├── README.md
│   └── workflow.json
├── tasks/                   # Internship tasks & phased deliverables
│   └── task2-whatsapp-phase1/
│       ├── config.json
│       ├── flow.mmd
│       ├── messages.md
│       ├── workflow.json
│       └── README.md
└── README.md                # Main internship documentation & progress log
```
