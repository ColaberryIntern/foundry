# Foundry — the Open House "wow" engine

**You're not watching me code. You're watching me build a company in real time.** 🚀

Foundry turns one sentence from an audience member — *"I own a landscaping company"* — into a complete, clickable, running AI company: a redesigned marketing **website** (hero + your services in the nav), executive **dashboards**, a Salesforce-style drag-and-drop **CRM**, a **Trust dashboard** (INPACT / GOALS), a searchable **Knowledge Base** with the **Cory** chatbot and downloadable one-pagers, a 25+ AI/human **workforce**, a business-process **database**, a **finance model**, a **roadmap**, and a source scaffold — all in the **light Colaberry brand** (Cherry/Leaf/Berry, with a dark toggle), rich with **Mermaid** storytelling diagrams, and unified by a single **Command Center** that opens in the browser at the reveal. Every answer the audience gives is **highlighted** across the company.

Then you turn to the room and say: *"That took twelve minutes. Our students spend twelve weeks learning to build it. This isn't the project — this is **Lesson One**."*

---

## The one-URL launch (this is the whole trick)

At the event, open Claude Code in an empty folder and paste this one line:

```
https://raw.githubusercontent.com/ColaberryIntern/foundry/main/START-HERE.md
```

Claude Code reads it and automatically: downloads the kit → **opens the interview in your browser** → waits. You fill the interview out with the room, click **Copy build prompt**, paste it back into Claude Code, and the company builds itself.

No typing, no remembering commands. One URL in, a whole company out.

---

## What's in this folder

| File | What it is |
|------|-----------|
| **START-HERE.md** | The agent bootstrap. The single URL you hand Claude Code — it auto-opens the interview, then builds. |
| **BusinessGenerator.md** | The master build spec. Claude Code reads this and generates the entire company. The engine. |
| **interview.md** | The live discovery worksheet you run with the audience. Fill it in, hand it to Claude Code. |
| **Interview.html** | A polished, projectable version of the interview. Fill it in live on screen → click **Copy answers**. |
| **templates/command-center.html** | The reference CEO cockpit. Renders as-is (sample company) and is the template Claude Code personalizes. Double-click it now to see the target experience. |
| **README.md** | This file — quick start + your on-stage run-of-show. |

---

## Quick start

1. **Before the event (once):** open `BusinessGenerator.md` §15 and paste in your real references (AI Project Architect repo URL, curriculum links). Optional but makes it sharper. Also double-click `templates/command-center.html` to see the reveal experience.
2. **At the event:** open Claude Code in an empty folder and paste the one-URL line above. It downloads the kit and opens the interview automatically.
3. **Run the interview** on the projector, filling it in with the room. Save the name for the finale.
4. **Click "Copy build prompt"** on the final screen, switch to Claude Code, **paste, press Enter.**
5. **Present while it builds** (the folder tree grows on screen). When it finishes, the Command Center opens by itself. **Reveal.**

> **No internet at the venue?** Clone/copy this folder onto the machine ahead of time. Then skip the URL: just open `Interview.html`, and after copying the prompt, paste it into Claude Code running in this folder. Everything works fully offline.

> **Dry run:** `interview.md` ships with a ready-made sample ("Evergreen Grounds Co."). Build the whole company from it to rehearse — no audience needed.

---

## The run-of-show (≈12–45 min, scale to your slot)

**0:00 — Set the frame.** *"I'm not going to show you our curriculum. I'm going to show you what you'll be able to build by Week 12. Who here owns a business?"* Pick a volunteer.

**0:01 — Let the AI interview them.** Project `Interview.html`. *"I'm going to let the AI interview you."* Read the questions as the AI. Move fast — ~30s each. The room realizes: *this thing understands businesses.*

**0:05 — Name it together.** The last question. Build the company name with the room. Emotional peak.

**0:06 — Hit go.** Click **Copy build prompt** on the interview's final screen, paste into Claude Code, press Enter. **Now present** — talk over it. Don't narrate every file; let the console fly in the background. Keep the outcome hidden ("let's see what it built at the end").

Talking points while it builds:
- *"It's not writing a chatbot. It's hiring a company."*
- *"Watch the folders appear — that's Sales, that's Finance, that's the AI workforce."*
- *"Every student learns to build each one of these pieces."*

**~0:12 — The reveal.** The Command Center opens automatically. Click through live:
- **AI Employees** → *"It hired 27 of them. This one, the Lead Qualification Agent, is the one they said they'd clone."*
- **Automations** → *"Form → AI calls → books → CRM → proposal → invoice. Nobody touched it."*
- **Website** → *"And here's their new website. It's live."*
- **Finance / Roadmap** → *"Here's the money, and here's the 90-day plan."*

**The close.** *"That took about twelve minutes. Our students spend twelve weeks learning to build exactly what you just watched. This isn't the project. **This is Lesson One.**"*

---

## Why this works

- **Show the transformation, not the syllabus.** People buy who they'll *become*, not a list of modules.
- **A company, not a chatbot.** An org chart of AI employees is unforgettable; another chatbot is not.
- **Reliable, not improvised.** The spec + template library mean the live build looks the same, polished, every time — no praying the model invents a good layout on stage.
- **The reveal is Christmas morning.** Hidden build → one dramatic open.

---

## Tuning it

- **Shorter slot?** Tell Claude Code to build a "core set" — Command Center, AI Employees, Automations, Website, Executive Dashboard — and skip the rest. Edit the checklist in `BusinessGenerator.md` §13.
- **Different brand look?** Change the palette in `BusinessGenerator.md` §9 and the `:root` variables in `templates/command-center.html`.
- **Add templates** (dashboard, website, CRM) to `templates/` to make the live build even faster and more consistent — the spec will use them automatically (§11).
- **Keep the references current** in §15 so the workforce and learning path match the real program (Experience Studio, Composer, graph engine, Project Builder).

---

*Built for the Colaberry AI Leadership Accelerator Open House. Name it whatever you like — Foundry, Genesis, Enterprise Foundry, Launchpad — the machine doesn't care. The audience will remember the moment, not the logo.*
