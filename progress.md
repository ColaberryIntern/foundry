# Foundry — Progress & Status

**What this is:** the "build a company live" Open House kit. Hand Claude Code one URL, it opens a live interview, and from the audience's answers it generates a full clickable AI company that opens in the browser at the reveal.

**Repo:** github.com/ColaberryIntern/foundry (public) · **Owner:** Colaberry AI Leadership Accelerator · **Basecamp:** Reference Kits → Foundry (ticket 10103550092)

**Status:** ✅ Working end-to-end. Live-tested twice (Evergreen Grounds Co., Pipe Aladdin).

---

## How to run it (the live flow)

1. At the event, open Claude Code in an empty folder and paste one line:
   ```
   https://raw.githubusercontent.com/ColaberryIntern/foundry/main/START-HERE.md
   ```
2. Claude Code downloads the kit and **auto-opens the interview**.
3. Run the **7-question** interview with the room (project `Interview.html`).
4. Click **📋 Copy build prompt**, paste into Claude Code, press Enter.
5. Present while it builds (~15–20 min); the **Command Center opens itself** for the reveal.
6. End on the **🏛️ First Board Meeting** module — the close.

**Optional (once, on the presenter's laptop):** click **✨** in the interview and paste an **OpenAI or Anthropic** key so made-up industries auto-generate tailored options. Stored locally only; the ✨ button hides once set (Ctrl+Alt+K to re-open). Never committed.

---

## What a build produces (current artifact set)

Command Center (cockpit) + 16 modules, all light Colaberry theme, Cherry/Leaf/Berry, Mermaid diagrams, interview answers highlighted:

- **Website** — hero = the tagline, nav = the services
- **CRM** — Salesforce-style **drag-and-drop** pipeline
- **Trust Dashboard** — the **six INPACT™ elements** (detailed + talk-track), 7-layer Mermaid, GOALS™, 28→85 journey
- **Knowledge Base** — typed search + **Cory** chatbot + 3 downloadable one-pagers
- **Marketing** — Power-BI charts **+ 4-ad social gallery + real write-ups** (blog/press/email/captions)
- **Roadmap** — expanded: Gantt, 30/60/90 tables, hiring plan, KPIs, risks
- Dashboards (exec + ops), Sales funnel, Database (business-process + ER), Analytics, Finance, SOPs, Workforce org-chart, AI Employees (24+), Portals (customer + admin)
- **🏛️ First Board Meeting** — THE CLOSER: the AI leadership team briefs the founder, "Ask the board," ends on "This is Lesson One."
- `src/` scaffold + `docs/assumptions.md`

**Removed:** Learning Path and Deployment modules (the Board Meeting carries the close).

---

## Build timing (measured)

- **Pipe Aladdin** (full 27-artifact build, 7 parallel builders): **~17 min** wall-clock — ~4–5 min foundation (folders, `company.json`, Command Center) + ~12 min parallel page generation.
- To pace a ~20–25 min slot: the deeper Trust/Marketing/Roadmap + the Board Meeting add content and time; you can also add per-service pages or agent profile pages.
- Marketing creative is generated at **higher effort/model** than other pages (weak marketing copy is the most noticeable failure).

---

## Kit files

| File | Role |
|---|---|
| `START-HERE.md` | Agent bootstrap (the URL you paste) — downloads the kit + assets, opens the interview |
| `BusinessGenerator.md` | The master spec Claude Code follows (folder tree, all artifact specs, design system, validation, launch) |
| `Interview.html` | The projectable live interview (7 Qs, industry-aware + LLM options, tracker, clear button) |
| `interview.md` | Backup worksheet + sample |
| `templates/command-center.html` | The cockpit template (Trust + Knowledge + Board Meeting cards) |
| `assets/theme.css` | Colaberry Design System (light default + dark toggle) — copied into every build |
| `assets/mermaid.min.js` | Offline Mermaid (2.7 MB) — copied into every build |
| `README.md` | Quick start + on-stage run-of-show |
| `progress.md` | This file |

---

## Changelog

- **v4 (2026-07-16)** — Trust dashboard deepened to the six INPACT™ elements + presenter talk-track (from Ram's book); Marketing gains a 4-ad gallery + real write-ups (higher-effort generation); Roadmap expanded (Gantt, hiring, KPIs, risks); **added the First Board Meeting closer**; **removed Learning Path + Deployment**. Live-tested on **Pipe Aladdin**.
- **v3** — Interview trimmed to 7 presentation-visible questions; LLM option-generation for made-up industries (OpenAI or Anthropic key, local-only, ✨ hides once set); Clear-all button.
- **v2** — Light Colaberry theme + dark toggle; redesigned website; Salesforce CRM; Trust dashboard (replaced Automations); Knowledge Base + Cory; Mermaid throughout; question-highlighting. Interview: Colaberry logo, Open House badge, live CST clock, left tracker, assignment banner.
- **v1** — One-URL launch; BusinessGenerator spec; projectable interview with copy-prompt; rehearsal (Evergreen Grounds Co.) ~24 min.

---

## Open items

- Paste the real **AI Project Architect repo URL** + **curriculum/lesson links** into `BusinessGenerator.md` §15 so the generated workforce + references name the real program pieces.
- Optional: a small server-side proxy (Accelerator VPS) if you ever want the KB/interview LLM to be key-free and shareable rather than per-laptop.
