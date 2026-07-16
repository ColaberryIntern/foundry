# Foundry — Business Operating System Generator

> **What this is.** A complete, self-contained build specification. When you drag this file plus a filled-in `interview.md` into Claude Code and say *"Build everything,"* Claude Code follows this document end-to-end and generates an entire operating AI company — dashboards, portals, a CRM, a website, a mixed AI/human workforce, a database, a financial model, SOPs, a roadmap, and a source-code scaffold — all as browsable HTML, unified by a single **Command Center**, then opens it in the browser.
>
> This is the "wow" engine for the Open House. The audience does not watch code. They watch a company materialize.

---

## 0. One-line invocation

The operator drags `interview.md` (filled in) and this file into Claude Code and types exactly one instruction:

```
Read interview.md and BusinessGenerator.md. Build the entire company now.
Continue working until every artifact in the completion checklist exists and validates.
Then open CommandCenter/index.html in my default browser.
```

Everything below is what Claude Code does in response. **Do not ask the operator clarifying questions during a live demo.** If information is missing, make a confident, realistic assumption, note it in `docs/assumptions.md`, and keep building. Momentum is the product.

---

## 1. The prime directive

You are generating **a business, not a document.** Every decision optimizes for one moment: the operator clicks `CommandCenter/index.html`, and a stranger's off-the-cuff business idea is suddenly a real, clickable, running company on screen.

Three rules govern everything:

1. **Finish.** Never stop half-built. Never leave a dead link, a `TODO`, a "coming soon," or lorem ipsum. If an artifact is in the checklist (§13), it must exist, be populated with realistic content, and open cleanly in a browser.
2. **Make it feel expensive.** Power-BI-grade dashboards. Executive polish. Consistent design system on every page (§9). If it looks like a school project, we failed.
3. **Everything connects to the Command Center.** The Command Center is the front door. From it you can reach every artifact in ≤2 clicks, and every artifact has a "← Command Center" link home.

---

## 2. Operating principles

- **HTML-first.** Primary deliverables are self-contained `.html` files that render instantly with no build step, no server, and no internet. Inline all CSS and JS. Use CDN-free code. Charts are drawn with inline SVG or a tiny vanilla-JS canvas routine — never an external chart library.
- **Template-driven.** Where a template exists in `templates/`, copy it and fill its tokens rather than inventing layout from scratch. This makes the live build fast and visually consistent. If a template is missing, generate the page to the same design system (§9) and, if time allows, save a reusable copy back into `templates/`.
- **One data spine.** Everything personalizes from a single generated file, `data/company.json` (§10). Build that first; every page reads from the same source of truth so numbers never contradict each other across pages.
- **Realistic, not real.** Invent plausible names, numbers, customers, and metrics that a person in that industry would nod at. No `$0`, no "Customer 1," no `[placeholder]`. If you invent a fact, it must be internally consistent with `company.json`.
- **Offline & portable.** The entire output folder must work when double-clicked from disk with no network. Assets are inline or generated locally (SVG logos, CSS gradients, emoji). No remote fonts, scripts, or images.
- **Keep going until validated.** After building, run the validation pass (§13). If anything is missing or broken, fix it and re-validate. Only then launch the browser.
- **Silent flourish.** During a live demo the console is the spectacle — folders appearing, files being written. Write files in the dramatic order of §5 so the tree "grows" like a company being founded.

---

## 3. Inputs

Read `interview.md`. It contains the audience's answers to a discovery interview (what the business does, customers, lead flow, tools, biggest time-sinks, the role to automate first, growth goal, and — near the end — the company name).

Parse those answers into structured facts. If a field is blank or ambiguous:
- Infer the most likely realistic value from the industry.
- Record every inference in `docs/assumptions.md` as `Assumed: <field> = <value> because <reason>.`
- Never block on a missing answer.

If `interview.md` is essentially empty (a dry run), invent a vivid sample business — a regional **landscaping company**, "Evergreen Grounds Co." — and build the full company from that so the demo still works.

---

## 4. Output folder structure

Create this exact tree inside a new folder named for the company (kebab-cased), e.g. `evergreen-grounds-co/`:

```
<company-slug>/
├── CommandCenter/
│   └── index.html            ← THE hero page. The CEO cockpit. Launch target.
├── data/
│   └── company.json          ← single source of truth (build FIRST)
├── dashboards/
│   ├── executive.html        ← Power-BI-style KPI dashboard
│   ├── sales.html
│   ├── marketing.html
│   ├── operations.html
│   └── finance.html
├── website/
│   └── index.html            ← customer-facing marketing site
├── portals/
│   ├── customer-portal.html  ← what a customer logs into
│   └── admin-portal.html     ← internal staff/employee portal
├── crm/
│   └── index.html            ← pipeline, contacts, deals
├── workforce/
│   ├── org-chart.html        ← AI + human org chart (25+ roles)
│   └── ai-employees.html     ← the AI workforce, each as a "hire card"
├── automations/
│   └── index.html            ← end-to-end workflow diagrams (form→call→book→invoice…)
├── marketing/
│   └── plan.html             ← campaigns, channels, funnel
├── sales/
│   └── funnel.html           ← stages, scripts, conversion math
├── database/
│   └── schema.html           ← ER diagram + tables + sample rows
├── analytics/
│   └── index.html            ← trends, cohorts, forecasts
├── sops/
│   └── index.html            ← standard operating procedures library
├── finance/
│   └── model.html            ← revenue/cost/cash model, 12-month projection
├── roadmap/
│   └── index.html            ← 90-day + 12-month roadmap
├── learning/
│   └── path.html             ← maps each artifact → the Accelerator lesson that builds it
├── src/
│   ├── README.md             ← what the real codebase would be
│   ├── CLAUDE.md             ← agent operating instructions for the real build
│   └── architecture.html     ← system architecture diagram
├── docs/
│   ├── deployment.html       ← how to ship it
│   └── assumptions.md        ← every inference you made
└── assets/
    └── theme.css             ← the shared design system (linked by every page OR inlined)
```

> If a page is easier to keep self-contained, inline `theme.css` instead of linking it. Portability beats DRY. Never let a page depend on a file that might not load from `file://`.

---

## 5. Generation workflow (build in this order)

Build in the order that makes the growing folder tree tell a story, and that guarantees data consistency.

**Phase A — Foundation (the spine)**
1. Parse `interview.md` → write `data/company.json` (§10). This locks every number and name.
2. Write `assets/theme.css` (§9) so every subsequent page inherits the look.
3. Write `docs/assumptions.md` (start it now; append as you go).

**Phase B — The people (who runs it)**
4. Generate the mixed AI/human **workforce** of **≥25 differentiated roles** (§6) into `company.json`, then render `workforce/org-chart.html` and `workforce/ai-employees.html`.

**Phase C — The machine (how it runs)**
5. `automations/index.html` — the end-to-end workflows.
6. `crm/index.html`, `sales/funnel.html`, `marketing/plan.html`.
7. `database/schema.html`, `src/architecture.html`.

**Phase D — The face (what the world sees)**
8. `website/index.html`, `portals/customer-portal.html`, `portals/admin-portal.html`.

**Phase E — The intelligence (how it's measured)**
9. `dashboards/executive.html` + the four department dashboards.
10. `analytics/index.html`, `finance/model.html`.

**Phase F — The plan (where it goes)**
11. `sops/index.html`, `roadmap/index.html`, `learning/path.html`.
12. `src/README.md`, `src/CLAUDE.md`, `docs/deployment.html`.

**Phase G — The cockpit (tie it all together)**
13. `CommandCenter/index.html` LAST, wired to every artifact above.

**Phase H — Prove it & reveal**
14. Run validation (§13). Fix anything missing. Re-validate.
15. Launch `CommandCenter/index.html` in the default browser (§14).

---

## 6. The workforce — a mixed AI + human company (≥25 roles)

The most memorable idea in the demo: *"Let's replace one employee"* → then reveal an entire company of them. Generate a complete workforce.

**Requirements**
- **At least 25 roles**, clearly differentiated by title, department, responsibilities, and whether each is an **AI Employee** or a **Human** role.
- Bias toward AI for repetitive/analytical/24-7 functions; keep humans for judgment, relationships, craft, and physical work. A realistic company is a *blend*, and the blend is the teaching point.
- The role named in the interview as "the one to automate first" is the **flagship AI Employee** — give it the richest detail.

**For each role, store in `company.json`:**
```
{
  "title": "Lead Qualification Agent",
  "type": "ai",                      // "ai" | "human"
  "department": "Sales",
  "reports_to": "Sales Director",
  "mission": "Respond to every inbound lead in under 60 seconds, qualify, and book.",
  "responsibilities": ["…","…","…"],
  "channels": ["email","sms","voice"],          // AI only
  "tools": ["CRM","Calendar","Knowledge Base"], // AI only
  "kpis": ["First-response time","Qualified-lead rate","Booked appts"],
  "hourly_equivalent": "$0 marginal, always-on",
  "human_backup": "Sales Director for exceptions"
}
```

**Suggested departments to populate (adapt to the industry):**
Executive (CEO, COO/Ops Director, CFO), Sales (Director + Lead Qual Agent + SDR Agent + Proposal Agent), Marketing (Director + Content Agent + Social Agent + SEO/Ads Agent + Brand Designer), Customer Success (Manager + Support Agent + Onboarding Agent + Review/Reputation Agent), Operations (Ops Manager + Scheduling/Dispatch Agent + Field Techs/Crew + Quality Agent), Finance (Bookkeeping Agent + Invoicing Agent + Collections Agent + FP&A Agent), People (Recruiting Agent + Training Agent), Data/IT (Data Analyst Agent + Systems/Automation Engineer).

**Render**
- `workforce/org-chart.html`: a clean top-down org chart. AI roles get a distinct badge/accent (e.g. a glowing chip labeled `AI`); humans get a neutral chip labeled `HUMAN`. Group by department. Lines connect reports.
- `workforce/ai-employees.html`: one polished "hire card" per AI Employee — avatar (generated SVG monogram), title, mission, channels, tools, KPIs, and a status pill (`● Active`). This is the page that makes people say *"it hired a whole company."*

> If an **AI Project Architect** reference repository is provided in §15, follow its role taxonomy and naming conventions so the generated workforce matches the program's canonical model.

---

## 7. Artifact specifications

Every page shares the header/footer, nav-home link, and design system (§9). Below is what each must actually contain. Fill with realistic, industry-specific content driven by `company.json`.

### 7.1 Command Center — `CommandCenter/index.html` (the hero)
The CEO cockpit. See §8 — it has its own full spec because it matters most.

### 7.2 Executive dashboard — `dashboards/executive.html`
Power-BI aesthetic. Above the fold: a **KPI tile row** (Revenue, Customers, Pipeline, Conversion, AI Employees, CSAT). Below: 3–4 charts drawn in inline SVG — a revenue trend line (12 months), a pipeline funnel, a channel-mix donut, a leads-by-week bar. A right rail of "AI reasoning" notes ("Marketing spend up 18% → 32 new leads; recommend reallocating $400 to referrals"). Everything reads from `company.json`.

### 7.3 Department dashboards — `sales.html`, `marketing.html`, `operations.html`, `finance.html`
Same skeleton as executive, scoped to the department's KPIs and charts. Sales: pipeline by stage, win rate, avg deal, top reps (incl. the Lead Qual Agent). Marketing: CAC, channel ROI, campaign table. Operations: jobs scheduled, on-time %, crew utilization, dispatch map (stylized). Finance: MRR/revenue, gross margin, cash runway, AR aging.

### 7.4 Website — `website/index.html`
A genuinely attractive customer-facing marketing site for the business: hero with value prop and CTA, services/products, social proof (invented but believable testimonials with names + towns), a pricing or "get a quote" section, and a contact form (non-functional but styled). This is what the audience "visits" at the reveal.

### 7.5 Portals — `portals/customer-portal.html`, `portals/admin-portal.html`
- **Customer portal:** logged-in view for a sample customer — upcoming appointments, invoices/payments, messages, documents, a "request service" button. Show a realistic named customer from the CRM.
- **Admin portal:** the internal staff view — today's schedule/dispatch, task queue (with AI Employees actively working items), inbox, quick actions. Convey "the business is running right now."

### 7.6 CRM — `crm/index.html`
A working-looking CRM: a **kanban pipeline** (Lead → Qualified → Quoted → Won/Lost) with draggable-looking cards, a contacts table (10–20 realistic rows), and a deal detail panel. Each card shows which AI Employee last touched it.

### 7.7 Automations — `automations/index.html`
The money slide. Render the end-to-end flows as clean vertical/branching diagrams (inline SVG or styled flow blocks):
`Customer submits form → AI qualifies → AI calls & books → CRM updates → Proposal generated → Owner notified → Reminder scheduled → Invoice created → Review requested.`
Include 2–4 flows relevant to the business. Each node labeled with the responsible AI Employee. This diagram, on its own, sells the course.

### 7.8 Marketing plan — `marketing/plan.html`
Channels (SEO, local ads, referrals, social, email), a 90-day campaign calendar, target CAC/LTV, content themes, and the funnel from awareness → booked. Tie each channel to a marketing AI Employee.

### 7.9 Sales funnel — `sales/funnel.html`
Visual funnel with real conversion math (leads → contacted → qualified → quoted → won, with % and counts that reconcile with `company.json`), plus a short discovery-call script the Lead Qual Agent uses.

### 7.10 Database — `database/schema.html`
An ER-style diagram (boxes + relationship lines in SVG/HTML) for the core entities (Customers, Leads, Jobs/Orders, Invoices, Employees, Appointments, Products…), each table with columns/types and 2–3 sample rows. Convey a real data model, not a toy.

### 7.11 Analytics — `analytics/index.html`
Trends, a simple cohort/retention view, a seasonality note, and a 90-day forecast with an "AI insight" callout per chart. Numbers reconcile with dashboards.

### 7.12 SOPs — `sops/index.html`
A library of 6–10 standard operating procedures the company runs on (e.g. "New Lead Intake," "Quote → Job Conversion," "Job Completion & Invoicing," "Review Request," "Weekly Financial Close"). Each SOP: trigger, steps, owner (often an AI Employee), and definition of done.

### 7.13 Finance model — `finance/model.html`
A 12-month projection table (revenue, COGS, gross margin, opex, net, cash) with an assumptions panel and a small chart. Show the impact of AI Employees as a cost line near $0 vs. the human-equivalent salaries they replace/augment. Make the ROI obvious.

### 7.14 Roadmap — `roadmap/index.html`
A **90-day plan** (30/60/90 milestones) and a **12-month roadmap** by quarter. Frame Day 1 = today. This is the "here's what happens after the open house" artifact.

### 7.15 Learning path — `learning/path.html`
The bridge to the program. For each major artifact generated, name the Accelerator lesson/week that teaches a student to build it themselves (Command Center → Experience Studio; AI Employees → Composer/Agents; automations → MCP servers & graph engine; the whole project → Project Builder). End with the line: **"You just watched Lesson One."** (See §15 for canonical curriculum references.)

### 7.16 Source & architecture — `src/README.md`, `src/CLAUDE.md`, `src/architecture.html`
- `architecture.html`: a system diagram (frontend, backend, database, AI agent layer, MCP servers, integrations).
- `README.md`: what the real repo would contain, how to run it, the stack.
- `CLAUDE.md`: the operating instructions a Claude Code agent would follow to actually build this company for real — closing the loop between demo and program.

### 7.17 Deployment — `docs/deployment.html`
The path from this folder to a live business: hosting, domain, environment, integrations (CRM, calendar, telephony, email/SMS, payments), a go-live checklist, and a "Day 1 operations" note.

---

## 8. The Command Center (full spec)

`CommandCenter/index.html` is the single most important page. Treat it as a product, not a link list. Use `templates/command-center.html` if present; otherwise build to this spec.

**Above the fold**
- Company name + generated SVG logo (monogram in the brand accent).
- A one-line positioning statement.
- A **KPI hero row** (5–6 tiles): Revenue, Customers, Employees (human), AI Employees, Market/Region, plus one signature metric for the industry.

**The module grid**
- A responsive grid of large, clickable cards — one per major artifact area: **Executive Dashboard, Website, CRM, Marketing, Sales, Finance, Operations, Analytics, Workforce, Automations, Database, SOPs, Roadmap, Learning Path, Architecture, Deployment.**
- Each card: icon (emoji or inline SVG), title, one-line description, and a live-looking stat. Entire card links to the artifact. Hover lifts the card.

**The "alive" touches (make it feel autonomous)**
- A subtle **AI activity ticker** near the top that cycles through believable events: *"Lead Qualification Agent booked an appointment · 2s ago"*, *"Invoicing Agent sent invoice #1043 · 11s ago"*, *"Marketing Agent published a blog post · 34s ago."* Pure front-end JS cycling a scripted list from `company.json` — no network.
- Small "● Active" status pills on the workforce card.
- Everything readable from across a room (large type, high contrast) because it will be **projected**.

**Craft**
- Dark, executive theme by default (looks premium on a projector). Fully offline. Loads instantly. No layout shift. Works at 1080p and 4K.

---

## 9. Design system (make everything look like one product)

Write `assets/theme.css` and apply it (linked or inlined) to every page. All pages must look like modules of the same platform.

**Palette (dark executive default)**
- Background: `#0B1220` (deep navy-black) with a subtle radial gradient toward `#111a2e`.
- Surface/cards: `#141d31` with `1px` border `#243049`.
- Text: primary `#E8EDF6`, muted `#94A3B8`.
- Brand accent: `#4F8CFF` (electric blue). Secondary accent: `#22D3A6` (emerald) for AI/positive, `#F5A524` (amber) for attention.
- Success `#22C55E`, warning `#F59E0B`, danger `#EF4444`.
- Derive a per-company accent from the industry if it strengthens identity (e.g. emerald for landscaping) but keep contrast AA+.

**Typography**
- System font stack only (offline): `-apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`. Numbers/labels may use a mono stack for a "dashboard" feel.
- Scale: hero 40–56px, section 24–28px, body 15–16px, KPI numbers 32–44px bold.

**Components (consistent everywhere)**
- **KPI tile:** label (muted, uppercase, letter-spaced), big number, small delta chip (▲/▼ colored).
- **Card:** rounded `16px`, soft shadow, `1px` border, hover lift + accent border.
- **Chart:** inline SVG, gridlines in low-opacity, accent stroke, area fill at ~12% opacity.
- **Badge/pill:** rounded-full, small caps — `AI` (emerald), `HUMAN` (slate), `● Active` (green dot).
- **Top bar** on every non-Command-Center page: left = company logo/name, right = "← Command Center" link.
- Generous spacing (24–32px), 12-column responsive grid, `max-width: 1200px` centered.
- Respect `prefers-reduced-motion`; keep animations subtle (fades, 150–250ms).

**Accessibility & responsiveness**
- AA contrast minimum. Focus states visible. All content reflows to a single column on narrow screens; wide tables/diagrams scroll inside their own container so the page never scrolls sideways.

---

## 10. The data spine — `data/company.json`

Build this **first**. Every page reads from it so nothing contradicts. Minimum shape:

```json
{
  "company": {
    "name": "",
    "slug": "",
    "tagline": "",
    "industry": "",
    "region": "",
    "founded": "today",
    "accent": "#22D3A6"
  },
  "positioning": { "problem": "", "promise": "", "differentiator": "" },
  "kpis": {
    "revenue_annual": 0, "revenue_mrr": 0, "customers": 0,
    "pipeline_value": 0, "conversion_rate": 0.0, "csat": 0.0,
    "human_employees": 0, "ai_employees": 0, "avg_deal": 0, "cac": 0, "ltv": 0
  },
  "revenue_trend_12mo": [/* 12 numbers */],
  "channels": [{ "name": "", "leads": 0, "cac": 0, "roi": 0 }],
  "pipeline": [{ "stage": "Lead", "count": 0, "value": 0 }],
  "workforce": [/* ≥25 role objects per §6 */],
  "customers_sample": [{ "name": "", "town": "", "value": 0, "status": "" }],
  "automations": [{ "name": "", "steps": ["", ""], "owner": "" }],
  "sops": [{ "name": "", "trigger": "", "steps": [], "owner": "", "dod": "" }],
  "finance_12mo": [{ "month": "", "revenue": 0, "cogs": 0, "opex": 0, "net": 0, "cash": 0 }],
  "roadmap": { "d30": [], "d60": [], "d90": [], "quarters": [] },
  "learning_map": [{ "artifact": "", "lesson": "" }],
  "activity_feed": ["Lead Qualification Agent booked an appointment", "…"],
  "assumptions": []
}
```

Fill every field with realistic, internally consistent values. Cross-check: `pipeline` value ≈ reconciles with `avg_deal × counts`; `revenue_mrr × 12 ≈ revenue_annual`; funnel percentages multiply through correctly. If pages embed their own copy of the data for offline portability, generate that copy **from** `company.json` so it stays consistent.

---

## 11. Templates

Look in `templates/`. If a template exists for a page, copy it and replace its `{{TOKENS}}` with values from `company.json`. Provided/expected templates:

- `templates/command-center.html` — the CEO cockpit (tokens like `{{COMPANY_NAME}}`, `{{ACCENT}}`, `{{KPI_REVENUE}}`, `{{MODULE_CARDS}}`, `{{ACTIVITY_FEED}}`).
- (Optional, generate if absent and time allows:) `dashboard.html`, `website.html`, `portal.html`, `crm.html`, `org-chart.html`, `report.html`.

When a template is missing, build the page to the design system in §9 and — outside a time-pressured live demo — save a cleaned, tokenized copy back to `templates/` so the next generation is faster and even more consistent.

---

## 12. Voice, content & realism guardrails

- **No filler.** Zero lorem ipsum, zero "Lorem", zero "Coming soon", zero empty states, zero `#` dead links. Every link resolves to a real generated page.
- **Believable specifics.** Real-sounding customer names and towns, plausible dollar amounts for the industry and region, invoice numbers, appointment times, campaign names.
- **Consistent numbers.** All KPIs across all pages trace back to `company.json`.
- **Confident, human copy.** Write like a sharp operator, not a template. Short, concrete, benefit-led.
- **On-brand everywhere.** Same header, same theme, same components, same "← Command Center" link.
- **Tasteful "alive."** Motion is subtle and purposeful (activity ticker, hover lifts). Never gimmicky.

---

## 13. Validation & completion checklist

Before launching the browser, verify **every** item. If any fails, fix and re-run this list.

**Files exist and are non-trivial (each > 2 KB of real content):**
- [ ] `data/company.json` — valid JSON, all sections populated, numbers reconcile
- [ ] `CommandCenter/index.html`
- [ ] `dashboards/executive.html`, `sales.html`, `marketing.html`, `operations.html`, `finance.html`
- [ ] `website/index.html`
- [ ] `portals/customer-portal.html`, `portals/admin-portal.html`
- [ ] `crm/index.html`
- [ ] `workforce/org-chart.html`, `workforce/ai-employees.html`  (≥25 roles, AI/human mix)
- [ ] `automations/index.html`
- [ ] `marketing/plan.html`, `sales/funnel.html`
- [ ] `database/schema.html`
- [ ] `analytics/index.html`
- [ ] `sops/index.html`  (≥6 SOPs)
- [ ] `finance/model.html`  (12-month table)
- [ ] `roadmap/index.html`  (30/60/90 + quarters)
- [ ] `learning/path.html`  (every artifact mapped to a lesson)
- [ ] `src/README.md`, `src/CLAUDE.md`, `src/architecture.html`
- [ ] `docs/deployment.html`, `docs/assumptions.md`
- [ ] `assets/theme.css` (or inlined equivalent on every page)

**Integrity checks:**
- [ ] Every module card on the Command Center links to a file that exists.
- [ ] Every non-Command-Center page has a working "← Command Center" link.
- [ ] No dead links, no `href="#"`, no `TODO`, no lorem, no "placeholder".
- [ ] Every page renders with no console errors from `file://` (no remote assets).
- [ ] Numbers reconcile across Command Center, dashboards, finance, and analytics.
- [ ] Workforce has ≥25 roles with a realistic AI/human split; the interview's "automate-first" role is the flagship AI Employee.

If **any** box is unchecked, **keep working.** Do not report done and do not launch until the checklist is fully green.

---

## 14. Auto-launch

After validation passes, open the cockpit in the operator's default browser. Detect the OS and run the right command from the output folder:

- **Windows:** `start "" "CommandCenter\index.html"`  (PowerShell: `Start-Process ".\CommandCenter\index.html"`)
- **macOS:** `open CommandCenter/index.html`
- **Linux:** `xdg-open CommandCenter/index.html`

Then print a short, dramatic completion summary to the console: company name, number of artifacts generated, number of AI Employees hired, and the single line: **"Your company is live. This is Lesson One."**

---

## 15. References (operator: fill these in before the event)

Claude Code should treat the following as canonical when present. Paste the exact URLs/IDs so generation matches the program's real assets.

- **AI Project Architect repository:** `<paste repo URL>` — use its role taxonomy and project-scaffold conventions for the workforce (§6) and `src/` (§7.16).
- **Colaberry Design System (Aleem's "Design E"):** Basecamp doc `10031928327` — align colors, components, and layout language with the official student-platform design system where it strengthens the look.
- **Accelerator curriculum (12-week / 4-intensive, CCA-F):** `<paste doc/repo>` — use real lesson/week names in `learning/path.html` (§7.15). Canonical building blocks to name: **Experience Studio** (UI/component generation), **Composer** (AI Employees/agents), the **graph engine** (orchestration/automations), **Project Builder** (end-to-end project scaffold), and the **Claude Code-first workflow**.
- **Additional Basecamp design references:** `<paste links>` — pass through verbatim so Claude Code can use them as visual references.

> If a reference is not provided, proceed without it using the design system in §9 and the concept names above, and note the omission in `docs/assumptions.md`. Never block the build waiting on a reference.

---

## 16. Definition of done

You are done when — and only when — the operator's browser opens to a Command Center for a company that did not exist fifteen minutes ago, every module clicks through to a polished, populated artifact, the numbers agree everywhere, an AI workforce of 25+ is visibly "at work," and nothing anywhere says "coming soon."

Then the operator turns to the room and says:

> *"That took about twelve minutes. Our students spend twelve weeks learning to build what you just watched. This isn't the project — this is Lesson One."*
