# Project 2 — Phase 1: LangChain + LangGraph Learning Week

**DevSynt AI Automation Internship · Mentor: Afnan Shoukat**

---

## Overview

An interactive, fully static HTML + CSS learning page covering the LangChain + LangGraph fundamentals learning week. The page walks through six days of material — from what a chain is on Day 1 to a complete four-agent retail data pipeline spec on Day 6 — with explanations, SVG diagrams, code examples, and interactive tab navigation.

No server, no build step, no dependencies. Open `index.html` in a browser and it works.

---

## File Structure

```
project2-phase1/
├── index.html        ← All page content and interactivity (vanilla JS)
├── style.css         ← All styling — color system, typography, layout, responsive
├── README.md         ← This file
└── screenshots/      ← Browser screenshot proving the page renders
```

---

## How to Run

**Option 1 — Local (simplest)**
1. Clone or download this repo
2. Open `index.html` in any modern browser
3. Done — no install, no server required

**Option 2 — VS Code Live Server**
1. Install the "Live Server" extension in VS Code
2. Right-click `index.html` → "Open with Live Server"
3. Opens at `http://localhost:5500`

**Option 3 — Vercel (for sharing a live URL)**
1. Push the repo to GitHub
2. Import at https://vercel.com/import — select the repo, deploy
3. Share the live URL in your submission

---

## Content Overview

### Day 1 — What is LangChain?
- What a chain is and why it's better than a raw API call
- The 5-step pipeline: User Input → Prompt Template → LLM → Output Parser → Final Answer
- Key terms: LLM wrapper, LCEL, prompt template, chain
- Comparison table: Raw API vs. LangChain chain

### Day 2 — Prompt Templates & Output Parsers
- How templates enable reusable, DRY prompt code
- Why output parsers matter: free-flowing text → structured JSON
- Template → LLM → Parser flow diagram
- Key parsers: `StrOutputParser`, `JsonOutputParser`, Pydantic models

### Day 3 — Memory & Tool-Calling
- Why LLMs have no memory by default and how to fix it
- Tool-calling: giving the LLM access to external functions
- The ReAct loop: Reason → Act → Observe → Repeat
- Real example: weather query using a tool chain

### Day 4 — What is LangGraph?
- Chain vs. Graph vs. Agent: what each one is for
- Core concepts: nodes, edges, conditional edges, state
- Example: order status system with branching logic (In Stock / Out of Stock)
- Why LangGraph exists — what chains can't do

### Day 5 — Orchestrator Agents
- What an orchestrator agent is (the "manager" pattern)
- Multi-agent systems: each agent specializes, orchestrator routes
- Full flow diagram: User → Orchestrator → Specialist Agents → Aggregate → Response
- Real example: splitting a complex query across a Sales Agent and a Support Agent

### Day 6 — The Project: Retail Data Pipeline
- Full specification for the four-agent system being built
- Pipeline diagram: Raw CSV → Orchestrator → Clean → Analysis → Visualization
- Per-agent breakdown with responsibilities and pseudo-code
- Recommended build order (Clean first, then Analysis, then Orchestrator, Viz last)

---

## The 4 Agents (Day 6 Project Spec)

| # | Agent | Role | Status |
|---|-------|------|--------|
| 1 | **Orchestrator Agent** | Receives raw CSV, decides processing order, routes to each agent in sequence | Required |
| 2 | **Clean Agent** | Fixes missing values, corrects data types, removes duplicates and broken rows | Required |
| 3 | **Analysis Agent** | Generates total sales, best-selling products, sales by region/category, summary stats | Required |
| 4 | **Visualization Agent** | Produces bar, line, and pie charts from the analysis output | Bonus |

**Build order:** Clean → Analysis → Orchestrator → Visualization (only after the first three work end-to-end).

---

## Features

- **Tab navigation** — Click Day 1 through Day 6 to switch content; Day 6 has a distinct indigo tab
- **Inline navigation** — "Day 6: The Project →" button inside Day 5 links directly to the spec
- **SVG diagrams** — All six flowcharts are embedded SVGs, fully responsive, no clipping
- **Syntax-highlighted code blocks** — JetBrains Mono, dark background, readable at all sizes
- **Responsive layout** — CSS Grid + Flexbox, tested at 1200px / 768px / 480px
- **Scroll animations** — Cards animate in via IntersectionObserver on first view
- **Reduced-motion support** — Animations disabled when the OS setting is active
- **Print styles** — Nav and tabs hidden, all day content visible for PDF export

---

## Learning Outcomes

After reviewing this page you should be able to:

- Explain what a **chain** is and when to use one instead of a raw API call
- Describe how **prompt templates** and **output parsers** make LLM code reliable and reusable
- Explain why LLMs need **memory** and how **tool-calling** extends what they can do
- Define the core **LangGraph** concepts: nodes, edges, conditional edges, and state
- Describe the **orchestrator pattern** and why it's the standard for real multi-agent systems
- Outline the **four-agent retail pipeline** and the responsibility of each agent

---

## Key Resources

| Resource | URL |
|----------|-----|
| LangChain Docs | https://python.langchain.com/docs/introduction/ |
| LangChain Academy (free courses) | https://academy.langchain.com |
| LangGraph Docs | https://langchain-ai.github.io/langgraph/ |
| Multi-Agent Collaboration Tutorial | https://langchain-ai.github.io/langgraph/tutorials/multi_agent/multi-agent-collaboration/ |

---

## Technical Details

**Built with**
- HTML5 — semantic structure, no frameworks
- CSS3 — custom properties (`:root`), Grid, Flexbox, `clamp()` fluid type scale
- Vanilla JavaScript — tab switching, IntersectionObserver scroll animations
- Inline SVG — all six flowcharts, verified to render within their `viewBox` bounds

**Typography**
- Headings: [Syne](https://fonts.google.com/specimen/Syne) (800 weight)
- Body: [Inter](https://fonts.google.com/specimen/Inter) + Plus Jakarta Sans fallback
- Code: [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)

**Browser support**
- Chrome / Edge (latest 2)
- Firefox (latest 2)
- Safari (latest 2)
- iOS Safari / Chrome Mobile

**Performance**
- ~150 KB total (HTML + CSS, no external JS)
- Zero npm dependencies, zero CDN scripts
- All fonts loaded via a single Google Fonts request

---

## Reflection

This week clarified the distinction between the three levels of complexity in LangChain/LangGraph work. **Chains** are for predictable pipelines where every step is known upfront — fast, simple, and easy to debug. **Agents** add the ability to reason and choose tools, but they can be opaque. **LangGraph** bridges the gap: it gives you the adaptability of an agent with the visibility of a flowchart, which matters when systems get complex.

The orchestrator pattern — one coordinator agent routing to specialized workers — is the design that scales. It keeps each agent focused on a single job, makes failures easy to trace, and lets you add new agents without touching existing ones. That's exactly why it's the right approach for the upcoming retail data pipeline.

---

**Deadline:** Tuesday, 10:00 PM  
**Submission:** GitHub repo link + Vercel live URL + screenshot in `screenshots/`  
**Questions:** Contact Afnan (Mentor) between 2 PM – 10 PM
