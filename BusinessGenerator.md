# Foundry — Business Operating System Generator

> **What this is.** A complete, self-contained build specification. When you drag this file plus a filled-in `interview.md` (or paste the interview's build prompt) into Claude Code and say *"Build everything,"* Claude Code follows this document end-to-end and generates an entire operating AI company — a redesigned marketing **website**, executive **dashboards**, a Salesforce-style **CRM**, customer/admin **portals**, a mixed AI/human **workforce**, a **Trust dashboard**, a business-process **database**, a **finance model**, **SOPs**, a **roadmap**, and a **source scaffold** — all as browsable HTML, unified by a single **Command Center**, then opens it in the browser.
>
> This is the "wow" engine for the Open House. The audience does not watch code. They watch a company materialize — in **their** brand, telling **their** story back to them.

---

## 0. One-line invocation

The operator fills in the interview (see `Interview.html`), clicks **Copy build prompt**, and pastes it into Claude Code. That prompt already says, in effect:

```
Read interview.md and BusinessGenerator.md. Build the entire company now.
Continue until every artifact in the completion checklist exists and validates.
Then open CommandCenter/index.html in my default browser.
```

Everything below is what Claude Code does in response. **Do not ask the operator clarifying questions during a live demo.** If information is missing, make a confident, realistic assumption, note it in `docs/assumptions.md`, and keep building. Momentum is the product.

---

## 1. The prime directive

You are generating **a business, not a document.** Every decision optimizes for one moment: the operator clicks `CommandCenter/index.html`, and a stranger's off-the-cuff business idea is a real, clickable, running company on screen — in a polished light theme, with their services in the nav, their words in the hero, and their answers highlighted everywhere.

Four rules govern everything:

1. **Finish.** Never stop half-built. No dead links, no `TODO`, no "coming soon," no lorem ipsum. Every checklist artifact (§13) must exist, be populated with realistic content, and open cleanly in a browser.
2. **Make it feel expensive.** Power-BI-grade dashboards, a real marketing website, executive polish. Consistent Colaberry design system on every page (§9). If it looks like a school project, we failed.
3. **Tell their story back to them.** Everything the audience answered in the interview (§3) must visibly show up — services become the website nav, the tagline becomes the hero, the "clone this employee" answer becomes the flagship AI Employee — and every question-derived value is wrapped so it's **visibly highlighted** (§9.4). Use **Mermaid** diagrams for dynamic storytelling wherever a process, hierarchy, or flow is involved (§9.5).
4. **Everything connects to the Command Center.** It's the front door; every artifact is reachable in ≤2 clicks and links back home.

---

## 2. Operating principles

- **HTML-first.** Primary deliverables are self-contained `.html` files that render instantly with no build step and no internet (except the bundled Mermaid lib, which is local). Inline all page CSS/JS beyond the shared theme. Charts are inline SVG (see §7.8) or Mermaid; never an external chart library.
- **Use the provided assets — do not regenerate them.** The kit ships `assets/theme.css` (the Colaberry design system, light + dark) and `assets/mermaid.min.js` (offline Mermaid). **Copy both into the company's `assets/` folder** and link them; do not hand-write a theme.
- **Light is the default; dark is a toggle.** Every page loads in the light Colaberry theme and includes the theme toggle (§9.3).
- **One data spine.** Everything personalizes from `data/company.json` (§10). Build it first so numbers never contradict across pages.
- **Realistic, not real.** Invent plausible names, numbers, customers, metrics a person in that industry would nod at. No `$0`, no "Customer 1," no `[placeholder]`.
- **Story-driven & highlighted.** Wrap every value that came from an interview answer in the highlight markup (§9.4) so the audience sees their own words called out across the company.
- **Offline & portable.** The whole output folder works double-clicked from disk with no network. Assets are inline, generated locally (SVG), or the two bundled files.
- **Keep going until validated.** After building, run §13. Fix anything missing/broken, re-validate, then launch the browser.
- **Silent flourish.** Write files in the dramatic order of §5 so the tree "grows" like a company being founded.

---

## 3. Inputs

Read `interview.md` (or the pasted build prompt). It carries the audience's answers, including new website-shaping fields:

| Field | Feeds |
|---|---|
| `company_does` | industry, positioning, everything |
| `services` (a list) | **website nav + services section**, SOPs, org |
| `customers` | CRM, website tone, marketing, testimonials |
| `tagline` | **website hero headline** |
| `clone_this_employee` | **flagship AI Employee** |
| `accent` | brand accent (Cherry / Leaf / Berry) |
| `company_name` | the name |

Only these **7** are asked — the interview is deliberately short, and every question is something you'll *see* in the walkthrough. **Infer everything else realistically from the industry** (region, pricing, team size, lead sources, revenue model, the roadmap) and record the inferences in `docs/assumptions.md`.

Parse into structured facts. Blank/ambiguous → infer realistically, record in `docs/assumptions.md`, never block. If the interview is essentially empty (a dry run), invent a vivid **residential landscaping** company, "Evergreen Grounds Co.," and build the full company from it.

---

## 4. Output folder structure

Create this tree inside a new folder named for the company (kebab-cased), e.g. `evergreen-grounds-co/`:

```
<company-slug>/
├── CommandCenter/index.html    ← THE hero page. Launch target.
├── data/company.json           ← single source of truth (build FIRST)
├── assets/
│   ├── theme.css               ← COPIED from the kit (do not regenerate)
│   └── mermaid.min.js          ← COPIED from the kit (offline Mermaid)
├── website/index.html          ← redesigned marketing site (hero + services nav)
├── dashboards/
│   ├── executive.html          ← Power-BI-style KPI dashboard
│   ├── operations.html
│   └── (sales/marketing live in marketing/ + sales/)
├── crm/index.html              ← Salesforce-style drag-and-drop pipeline
├── portals/customer-portal.html, admin-portal.html
├── workforce/org-chart.html, ai-employees.html
├── trust/index.html            ← TRUST dashboard (INPACT · 7-Layer · GOALS)
├── marketing/plan.html         ← Power BI charts, channels, funnel
├── sales/funnel.html
├── database/schema.html        ← how the business works (Mermaid) + ER + data
├── analytics/index.html
├── knowledge/index.html        ← searchable KB + "Cory" chatbot + 3 one-pager docs (downloadable)
├── sops/index.html
├── finance/model.html
├── roadmap/index.html          ← expanded plan (§7.14): Gantt, hiring, KPIs, risks
├── boardroom/index.html        ← THE CLOSER (§7.15): AI board meeting + "Ask the board"
├── src/README.md, CLAUDE.md, architecture.html
├── docs/assumptions.md
```

> Note: there is **no `automations/` folder** — the end-to-end flows now live inside the **Trust dashboard** and the **database** page as Mermaid diagrams.

---

## 5. Generation workflow (build in this order)

**Phase A — Foundation (the spine)**
1. Parse the interview → write `data/company.json` (§10). Locks every name and number.
2. **Copy** `assets/theme.css` and `assets/mermaid.min.js` from the kit into the company's `assets/`.
3. Start `docs/assumptions.md`.

**Phase B — The people** — 4. workforce (§6) → `workforce/org-chart.html`, `ai-employees.html`.

**Phase C — The face & the machine** — 5. `website/index.html` (§7.4). 6. `crm/index.html` (§7.6). 7. `database/schema.html` (§7.10). 8. `trust/index.html` (§7.7).

**Phase D — Intelligence** — 9. `dashboards/executive.html` + `operations.html`; `marketing/plan.html`; `sales/funnel.html`; `analytics/index.html`; `finance/model.html`.

**Phase E — The plan & the hub** — 10. `sops`, `roadmap`, `portals`, `src/*`. 11. `knowledge/index.html` (§7.18) — built after the other artifacts so it can index them.

**Phase F — The closer & the cockpit** — 12. `boardroom/index.html` (§7.15) — the finale. 13. `CommandCenter/index.html` LAST, wired to every artifact (§8).

**Phase G — Prove it & reveal** — 12. Validate (§13). Fix. Re-validate. 13. Launch the Command Center (§14).

---

## 6. The workforce — a mixed AI + human company (≥25 roles)

Generate a complete workforce of **≥25 roles**, clearly differentiated by title, department, and **type** (`ai` | `human`). Bias AI toward repetitive/analytical/24-7 work; keep humans for judgment, relationships, craft, physical work. The `clone_this_employee` answer becomes the **flagship AI Employee** (richest detail). **Compute AI/human counts by counting the array — never hard-code a total that can drift** (§12). Include a **Governance / Trust Agent** so the Trust dashboard (§7.7) has an owner.

Per role store: `title, type, department, reports_to, mission, responsibilities, channels[], tools[], kpis[], flagship?`.

Render `workforce/org-chart.html` (top-down, AI vs HUMAN badges, grouped by department, a **Mermaid `graph TD`** version of the hierarchy) and `workforce/ai-employees.html` (one polished "hire card" per AI Employee — SVG monogram, mission, channels/tools pills, KPIs, `● Active`).

---

## 7. Artifact specifications

Every page: links `../assets/theme.css`, opens with the standard top bar + theme toggle (§9.3), uses Colaberry components, highlights question-derived values (§9.4), and uses Mermaid for any process/flow/hierarchy (§9.5). Fill with realistic, industry-specific content from `company.json`.

### 7.1 Command Center — `CommandCenter/index.html`
See §8. Use `templates/command-center.html`, personalized.

### 7.2–7.3 Dashboards — `dashboards/executive.html`, `operations.html`
Power-BI aesthetic on light surfaces. Executive: KPI tile row (Revenue, Customers, AI Employees, Trust/INPACT, Pipeline, CSAT) + 4 inline-SVG charts (revenue trend, pipeline funnel, channel mix, leads/week) + an "AI reasoning" rail. Operations: jobs, on-time %, crew utilization, a stylized dispatch view, today's schedule table.

### 7.4 Website — `website/index.html` (redesign — make it significant)
This is the front door; make it look like a real, modern marketing site, adapting the Colaberry marketing-kit patterns.
- **Sticky top nav** with the company name/logo on the left and **one nav item per service** from the `services` answer (anchor links to sections), plus a "Get a quote" button. The services in the nav must be visibly the audience's answers.
- **Hero** with: an eyebrow, the **`tagline`** answer as the H1 (highlighted), a supporting line, two CTAs, and a **hero visual** — a tasteful inline-SVG scene appropriate to the industry (for landscaping: sky/hill/house/lawn) with a floating stat chip or two. (If the venue has internet you may swap in a real industry photo; default to the self-contained SVG.)
- **Trust strip** under the hero: rating, customer count, "licensed & insured," years — pulled from `company.json`.
- **Services section**: one card per service (from `services`), each with a one-line benefit. This section is the payoff of the nav.
- **"Who we serve"** reflecting the `customers` answer; **"How it works"** 3-step; **social proof** (3 testimonials using real names/towns from `customers_sample`); **service-area** line from `region`; a **"Get a free quote"** section with a styled (non-submitting) form.
- Everything that came from an answer (services, tagline, customers, region) is wrapped in `.hl` and, for the hero and services, tagged with a small `.qtag` "from your interview" so the audience sees their words. Accent = the `accent` answer (Cherry/Leaf/Berry).

### 7.5 Portals — `portals/customer-portal.html`, `admin-portal.html`
Customer: a named sample customer's appointments, invoices/payments (one paid, one due), messages, documents, "request service." Admin: today's dispatch, a task queue with AI Employees actively working items, inbox, quick actions — "the business is running right now."

### 7.6 CRM — `crm/index.html` (Salesforce-style, drag-and-drop)
Build a CRM that reads like Salesforce and **is demoable live**:
- A **kanban pipeline** with stage columns (New Lead → Qualified → Quoted → Won / Lost). Each column shows a count and summed value in its header.
- **Deal cards are draggable** (native HTML5 drag-and-drop): the operator can drag a card from one stage to another during the demo, and the column counts/totals **update live** as cards move. Cards show contact, deal value, and "last touched by <AI agent>."
- A left rail of objects (Leads, Contacts, Accounts, Opportunities) and a Salesforce-like top utility bar for authenticity (visual only).
- Below the board, a **contacts table** from `customers_sample`.
- Include a tiny "▶ Demo: auto-advance a deal" button that programmatically moves one card a stage, in case dragging is awkward on the projector.

### 7.7 Trust Dashboard — `trust/index.html` (the differentiator — build it DEEP)
Grounded in Colaberry's **Architecture of Trust** (from *Trust Before Intelligence*, Ram Katamaraja). The presenter discusses these principles on stage, so make it **detailed and quotable**, not a scorecard. Three pillars:

**INPACT™ — the six elements of trust (the centerpiece).** Frame it: *"Just as Tony Robbins named six human needs, INPACT™ names six architectural needs an AI must meet to earn trust. All six are required — miss one and you rejoin the 95% of AI projects that fail."* Show an overall **INPACT gauge (0–100, from `trust.inpact_score`)**, then a rich card for EACH of the six — letter, name, the **principle tagline**, "What it means", "Why it matters", the company's **score bar** (from `trust.inpact`), a **company-specific example** (from `trust.notes`), and the **target metric**:
- **I — Instant · "Speed builds confidence."** Respond in <2s (sub-second ideal); users bail after ~3s. Target: <2s p95.
- **N — Natural · "Understanding builds connection."** Understand plain language at 75–85%+; no special syntax. Target: 80%+ understanding.
- **P — Permitted · "Security builds safety."** Dynamic RBAC + ABAC authorization, audit trails, human-in-the-loop for critical actions. Target: ABAC <10ms + 100% audited.
- **A — Adaptive · "Improvement builds reliability."** Learns continuously from feedback (weekly, not quarterly). Target: weekly loop, 1–2%/wk gains.
- **C — Contextual · "Completeness builds accuracy."** Real-time data from 5–8+ systems, not one source. Target: 5+ sources, <1hr freshness.
- **T — Trusted · "Transparency builds confidence."** Full audit trails, citations, inspectable reasoning. Target: 100% audit + source citations.
Include a highlighted **"Talk track — the principles"** panel: 1–2 speakable one-liners per element for the human on stage.

**7-Layer Architecture — how it's built.** Storage → Real-Time → Semantic → Intelligence → Governance → Observability → Orchestration. A **Mermaid** `graph TD` stack, each layer ✅ with a one-line note, plus a needs→layers map ("Instant needs Layer 2; Permitted needs Layer 5; Trusted needs Layer 6").

**GOALS™ — how it's measured.** **G**overnance, **O**bservability, **A**vailability, **L**exicon, **S**olid — five tiles with values (`trust.goals`) and a one-line meaning each.

**Trust journey + workflow.** A **28 → 85 in 90 days, 477% ROI** callout tied to the roadmap, and a **Mermaid** flow of a trusted end-to-end workflow labeling each node with the INPACT dimension it satisfies. One-liner for the room: *"INPACT is the destination, the 7 layers are the vehicle, GOALS is the maintenance."*

### 7.8 Marketing — `marketing/plan.html` (reports **plus real creative**)
Three parts. **(1) Report wall:** a Power-BI-style set of 4–6 inline-SVG charts (channel-ROI bars, CAC-vs-LTV, spend donut, monthly-leads trend, conversion funnel), a channels table with a totals row, a 90-day campaign calendar, one tight "AI insight" per chart. **(2) Social ad gallery — 4 designed ads** (Instagram reel, Facebook retargeting, a real Google search-ad format, one premium/aspirational): each a proper creative mockup with an inline-SVG visual (not a gray box), platform chip, a scroll-stopping headline, tight body copy, and a CTA. **(3) Long-form write-ups (real, well-written copy):** a blog post (title + subheads + 5–7 crafted paragraphs + CTA), a proper press release (FOR IMMEDIATE RELEASE, dateline, lede, founder quote with personality, boilerplate, ###), an email (subject + 2 A/B alternates + preview + body), and 3 social captions with hooks + hashtags. Attribute each piece to the responsible marketing AI Employee (`.badge.ai`).
> **Creative bar (do not skimp):** headlines are short, concrete, with a hook or twist; body copy is specific (numbers, guarantees, real objections); every piece has a reason to act now. No "unlock / elevate / in today's fast-paced world," no AI hedging. Use the audience's `tagline` as a confident signature sign-off. Make it something the room would screenshot. **For the live build, generate this section with a stronger model / higher effort than the rest** — weak marketing copy is the most noticeable failure.

### 7.9 Sales — `sales/funnel.html`
A visual funnel with real math from `pipeline` (counts + stage %), average deal, pipeline value, and a short discovery-call script the flagship agent uses. Include a **Mermaid** sequence of a discovery call.

### 7.10 Database — `database/schema.html` (show how the business works)
Two layers:
1. **How the business runs** — a **Mermaid** business-process diagram (`graph TD` or `flowchart`) from lead to cash to repeat, showing the real operational flow, which agent/role owns each step, and where data is written. This is the "exactly how the business should work" view.
2. **The data model** — an ER diagram (Mermaid `erDiagram` and/or styled boxes) for Customers, Leads, Jobs, Invoices, Employees, Appointments, Products — columns/types + 2–3 sample rows each (use `customers_sample`).

### 7.11 Analytics — `analytics/index.html`
Trends, a cohort/retention view, seasonality note, a 90-day forecast, each chart with an "AI insight." Numbers reconcile with dashboards/finance.

### 7.12 SOPs — `sops/index.html`
6–10 SOPs (trigger, steps, owner — badge AI where applicable, definition of done). At least the top 2 SOPs also get a small **Mermaid** flow.

### 7.13 Finance — `finance/model.html`
A 12-month projection table (revenue, COGS, gross margin, opex, net, cash) + assumptions + a small SVG chart. A callout: the AI Employees cost ≈$0 marginal vs. the human-equivalent salaries (make ROI obvious; echo the book's "477% ROI" energy).

### 7.14 Roadmap — `roadmap/index.html` (a real operating plan — expand it)
Not a three-column list — a detailed plan: a **North Star** line (where the company is in 12 months) + a 3-metric from→to strip; a **Mermaid `gantt`** of the first two quarters (with a couple of dependencies); **30/60/90 initiative tables** where each row has Owner (a real role/AI Employee, `.badge.ai`), Dependency, Success metric (target), and Status; a **hiring & workforce plan** (when to add people/agents, vs. the ~$0 AI cost line); a **KPIs-by-phase** table (targets at Day 30/60/90); a **risks & mitigations** table (4–5 rows); and the **12-month, 4-quarter** roadmap with 3 key results each. Tie the arc to the Trust journey (INPACT 28→85). Make it long, scannable, and genuinely useful.

### 7.15 First Board Meeting — `boardroom/index.html` (THE CLOSER)
The finale a presenter clicks last, replacing the old Learning Path. The generated **AI leadership team convenes** to brief the founder (the audience volunteer):
- A "**Convene the board**" button that reveals ~6 AI executives one at a time (staggered) — theatrical.
- One card per exec (real roles from `workforce` — Chief of Staff, CFO, Sales Director, Marketing Director, Governance/Trust, and the flagship): SVG monogram, `● Active`, a **📈 one-line recommendation** and a **⚠️ one-line risk flag**, specific to this business.
- The **CEO's charge to the founder**: a crisp 90-day directive (3 priorities from the roadmap) ending on a rallying line that fits the tagline.
- **"Ask the board"** — a text box + 3 suggested questions; route each to the most relevant exec and answer from an embedded, offline knowledge set (no network).
- **The close:** a full-width banner — big **"This is Lesson One."** and the "built live in ~15 minutes / students spend twelve weeks" line. This carries the emotional button the Learning Path used to.

### 7.16 Source & architecture — `src/README.md`, `src/CLAUDE.md`, `src/architecture.html`
`architecture.html`: a system diagram (Mermaid) — surfaces → app/API → database → AI agent layer → MCP servers → integrations, mapped to the 7 trust layers. `README.md`/`CLAUDE.md`: what the real repo/agent would be, closing the loop between demo and program.

### 7.18 Knowledge Base — `knowledge/index.html` (search + "Cory" chatbot + one-pagers)
A single hub, modeled on Colaberry's enterprise knowledge base (`enterprise.colaberry.ai/knowledge`), that makes the whole company searchable and explainable. Build it **after** the other artifacts so it can index them. Everything is self-contained and offline.

**Layout:** a hero with a big **typed search box**, a row of domain filter tiles (Sales, Marketing, Operations, Finance, Workforce, Trust, …), a results list, a **document library** (the one-pagers), and a docked **Cory** chat panel.

**1. Typed search (offline, instant).** Embed a knowledge index in the page built from `company.json` + a generated **Q&A set (40–80 entries)** covering the company (what it does, services, pricing, who runs it, the AI workforce, the trust story, the numbers, the roadmap). As the operator types, rank and show matching entries live (title + snippet + domain tag). Clicking a result scrolls to the answer or opens the relevant one-pager. Pure JS ranking (token overlap / includes) — no backend.

**2. "Cory" chatbot (grounded).** A chat panel named **Cory** (Colaberry's KB assistant persona). Cory answers questions about the entire project from the **same embedded knowledge pack** (company.json + Q&A + one-pager text) so it "understands the whole company."
- **Default = offline retrieval:** on each question, rank the knowledge pack, compose a concise answer from the top passages, and cite which artifact it came from (with a link). Include 3–4 suggested starter questions. This must work with **no network** so it never fails on stage.
- **Optional LLM upgrade (RAG):** if a config object `window.FOUNDRY_LLM = { endpoint, model, apiKey }` is present, Cory instead sends the user question + the retrieved knowledge pack as context to that endpoint and streams the reply. Gate this behind the config so the page stays self-contained by default; never hard-code a key. Document the toggle in a comment.

**3. Documents — up to 3 one-pagers (with Mermaid, downloadable).** Generate up to **three** polished one-page documents about the company, each openable in a reader/modal from search or the library:
1. **Company Overview** — what it does, services, customers, positioning, the headline numbers, and a Mermaid "how the business works" snapshot.
2. **How It Works / Operations** — the lead-to-cash flow (Mermaid), the AI workforce at a glance, and the SOP highlights.
3. **The Trust Story** — the INPACT/GOALS scorecard and the 28→85 journey (Mermaid 7-layer), plus the ROI.
Each one-pager is print-clean (A4/Letter width, its own header) and has a **Download** button that (a) triggers `window.print()` for a save-as-PDF, and (b) offers a **self-contained HTML download** via a `Blob` + object URL so the operator can hand the file to the audience member. The **Company Overview** is the "download the one-pager of the company we created together" deliverable — make it genuinely shareable.

Highlight interview-derived values (`.hl`) throughout, and keep the whole page on the light Colaberry theme with the toggle.

---

## 8. The Command Center (full spec)

`CommandCenter/index.html` is the most important page. Use `templates/command-center.html` (already light-themed with the toggle and a **Trust Dashboard** card in place of Automations). Personalize: company name + SVG monogram, tagline, a **KPI hero row** (Revenue, Customers, AI Employees, **Trust/INPACT**, Pipeline, CSAT), a responsive **module grid** (one card per artifact area, including 🛡️ **Trust Dashboard** → `../trust/index.html`, 📚 **Knowledge Base** → `../knowledge/index.html`, and 🏛️ **First Board Meeting** → `../boardroom/index.html` as the closing card — **no Learning Path or Deployment cards**), an **AI activity ticker** (believable events from `company.json`, including a Governance/Trust event), and the closing "twelve minutes / twelve weeks" line. Large type, high contrast (it will be projected), light default with the toggle.

---

## 9. Design system — the Colaberry system (Design E)

**Do not invent a theme. Copy `assets/theme.css` and link it from every page.** It is the Colaberry Design System, light + dark.

### 9.1 Palette
- **Cherry Red `#FB2832`** (primary/brand accent), **Leaf Green `#77BB4A`/`#5BA63C`** (secondary/positive), **Berry Blue `#367895`** (tertiary/info/AI).
- Neutrals from `#FFFFFF`/`#F8F8F7` (light surfaces) to `#0F0F0F` (dark). **Light is the default**; text is near-black on white.
- Data-viz series: use the theme's `--chart-1…8` (color-blind-safe, theme-aware). Never use raw brand ramps for chart series.
- The `accent` interview answer picks which brand hue leads for that company (default Cherry).

### 9.2 Type & shape
- **Roboto** (display + body), **Roboto Mono** (data/figures) — font stacks fall back to system fonts offline (no web-font `@import`). Headings bold, tight tracking. Scale ~H1 42 / H2 32 / H3 24 / body 16.
- Rounded, friendly shapes (radius 8–24px), soft neutral shadows, 4px spacing grid.

### 9.3 Standard page chrome (every page)
In `<head>`, before styles:
```html
<script>(function(){var t=localStorage.getItem('foundry-theme')||'light';document.documentElement.setAttribute('data-theme',t);})();</script>
```
Set `<html lang="en" data-theme="light">`. Link `../assets/theme.css`. Open `<body>` with:
```html
<header class="topbar">
  <div class="logo">E</div><div class="co">Company Name</div>
  <span class="spacer"></span>
  <a class="home" href="../CommandCenter/index.html">← Command Center</a>
  <button class="theme-toggle" onclick="var d=document.documentElement,n=d.getAttribute('data-theme')==='dark'?'light':'dark';d.setAttribute('data-theme',n);localStorage.setItem('foundry-theme',n);this.textContent=n==='dark'?'☀️':'🌙';">🌙</button>
</header>
<div class="wrap"> … <h1 class="page">…</h1> <p class="sub">…</p> … </div>
```
Theme classes available: `.card .kpis/.kpi .badge.ai/.human/.active .tablewrap/table .flow/.node .pill .btn .mermaid .seclabel .hl .qtag`.

### 9.4 Highlight the audience's answers (required)
Wrap every value that came from an interview answer in `<span class="hl">…</span>`. For the hero headline and the services, also append a `<span class="qtag">from your interview</span>` once per section. Result: as you scroll any page, the audience literally sees their own words called out in Leaf-green highlight. Do this on the website, Command Center tagline, CRM (customer type), marketing (channels), Trust (the "keeps me up" → trust concern), and roadmap (the 90-day goal).

### 9.5 Mermaid storytelling (use it wherever there's a process)
Every page with a process, hierarchy, or flow includes at least one **Mermaid** diagram. Load the local lib once per page that uses it:
```html
<script src="../assets/mermaid.min.js"></script>
<script>mermaid.initialize({startTheme:'base', theme:'base', securityLevel:'loose',
  themeVariables:{fontFamily:'Roboto, system-ui, sans-serif', primaryColor:'#EAF2F6', primaryBorderColor:'#367895', primaryTextColor:'#1A1A1A', lineColor:'#8C8C8C'}});</script>
```
Put diagrams in `<pre class="mermaid"> … </pre>` inside a `.mermaid` card. Follow the **Colaberry Mermaid Codex**: diagrams are *maps, not books* (2–3 lines per node), **all node text bold** (`<b>…</b>`), `<br/>` for line breaks, high contrast, and **semantic color**: green/teal = good/solution/GOALS, red = problem/old way, neutral gray = context, orange = intermediate. Required diagrams: org hierarchy (workforce), 7-Layer architecture + trusted workflow (trust), business-process + ER (database), discovery call (sales), system architecture (src). Keep each simple and readable from across a room.

### 9.6 Accessibility & responsiveness
AA contrast (the tokens are audited). Visible focus. Single-column reflow on narrow screens; wide tables/diagrams scroll inside their own container so the page never scrolls sideways.

---

## 10. The data spine — `data/company.json`

Build first. Minimum shape (extend as needed):
```json
{
  "company": { "name":"","slug":"","monogram":"","tagline":"","industry":"","region":"","accent":"#FB2832" },
  "services": ["","",""],
  "positioning": { "problem":"","promise":"","differentiator":"" },
  "kpis": { "revenue_annual":0,"revenue_mrr":0,"customers":0,"pipeline_value":0,"conversion_rate":0.0,
            "csat":0.0,"human_employees":0,"ai_employees":0,"avg_deal":0,"cac":0,"ltv":0,"inpact_score":85 },
  "revenue_trend_12mo": [], "channels": [], "pipeline": [],
  "workforce": [ /* ≥25 roles per §6, incl. a Governance/Trust agent */ ],
  "customers_sample": [], "trust": { "inpact": {"I":0,"N":0,"P":0,"A":0,"C":0,"T":0},
    "goals": {"G":0,"O":0,"A":0,"L":0,"S":0}, "layers": [], "journey_from":28, "journey_to":85 },
  "sops": [], "finance_12mo": [], "roadmap": {}, "learning_map": [], "activity_feed": [], "assumptions": []
}
```
Derive `ai_employees`/`human_employees` by counting the `workforce` array. Cross-check reconciliation: `mrr×12≈annual`; funnel %s multiply through; pipeline value ≈ `avg_deal × counts`. Every page reads from here.

---

## 11. Templates & assets

- `templates/command-center.html` — the light-themed cockpit with the Trust card. Copy → `CommandCenter/index.html`, replace the `COMPANY` object with `company.json` values.
- `assets/theme.css`, `assets/mermaid.min.js` — copy verbatim into the company's `assets/`. Never regenerate the theme; never load Mermaid from a CDN.
- If you build a page with no template, follow §9 and, outside a live demo, you may save a reusable template back to `templates/`.

---

## 12. Voice, content & realism guardrails

- **No filler.** Zero lorem, "coming soon," empty states, or dead links.
- **Believable specifics.** Real-sounding names/towns, plausible dollar amounts, invoice numbers, campaign names.
- **Consistent numbers.** All KPIs trace to `company.json`. **Derive headcounts by counting the `workforce` array — never hard-code a total that can drift.** The Command Center, org chart, finance, and every "N AI Employees" mention show the same number.
- **Confident, human copy.** Short, concrete, benefit-led.
- **On-brand & highlighted.** Same top bar, theme, components, "← Command Center" link, and `.hl` on every answer-derived value.
- **Tasteful motion.** Activity ticker, hover lifts, subtle fades. Respect `prefers-reduced-motion`.

---

## 13. Validation & completion checklist

Before launching, verify **every** item. If any fails, fix and re-run.

**Files exist & are non-trivial:**
- [ ] `data/company.json` (valid JSON, populated, numbers reconcile)
- [ ] `assets/theme.css` **and** `assets/mermaid.min.js` copied in
- [ ] `CommandCenter/index.html`
- [ ] `website/index.html`  (hero + services nav from answers)
- [ ] `crm/index.html`  (draggable pipeline)
- [ ] `trust/index.html`  (INPACT gauge + **all six elements detailed** + talk-track panel + 7-Layer Mermaid + GOALS)
- [ ] `dashboards/executive.html`, `operations.html`
- [ ] `marketing/plan.html`  (≥4 Power-BI charts + **4-ad gallery + real write-ups**), `sales/funnel.html`
- [ ] `database/schema.html`  (business-process Mermaid + ER)
- [ ] `workforce/org-chart.html` (≥25 roles, AI/human mix, Mermaid), `ai-employees.html`
- [ ] `analytics/index.html`, `finance/model.html`, `sops/index.html`, `roadmap/index.html`  (expanded: Gantt + hiring + KPIs + risks)
- [ ] `knowledge/index.html`  (typed search + Cory chatbot + ≥3 one-pagers with Mermaid + working Download)
- [ ] `boardroom/index.html`  (AI board meeting + Ask-the-board + the "Lesson One" close)
- [ ] `portals/customer-portal.html`, `admin-portal.html`
- [ ] `src/README.md`, `CLAUDE.md`, `architecture.html`; `docs/assumptions.md`

**Integrity:**
- [ ] Every Command Center module card links to a file that exists (incl. Trust; no Automations link).
- [ ] Every page has the top bar, the **theme toggle**, and loads **light** by default.
- [ ] Every page links `../assets/theme.css`; Mermaid pages load `../assets/mermaid.min.js` and render (no CDN, no console errors from `file://`).
- [ ] Interview-derived values are wrapped in `.hl`; website nav = the `services` answer.
- [ ] Numbers reconcile across Command Center, dashboards, finance, analytics; headcounts counted from the array.
- [ ] No dead links, no `href="#"` for nav, no `TODO`/lorem/"placeholder"/"coming soon."

If **any** box is unchecked, **keep working.** Do not report done or launch until fully green.

---

## 14. Auto-launch

After validation, open the cockpit in the default browser from the output folder:
- **Windows:** `start "" "CommandCenter\index.html"` (PowerShell: `Start-Process ".\CommandCenter\index.html"`)
- **macOS:** `open CommandCenter/index.html` · **Linux:** `xdg-open CommandCenter/index.html`

Then print a short dramatic summary (company name, artifacts generated, AI Employees hired, INPACT score) and: **"Your company is live. This is Lesson One."**

---

## 15. References (canonical — use when present)

- **Colaberry Design System (Design E):** `github.com/aleemcolaberry/colaberry-design-system` — the source of `assets/theme.css` (Cherry/Leaf/Berry tokens, light+dark, data-viz palette, Roboto). BC: `10031928327`.
- **Trust Before Intelligence:** `github.com/colaberry/trust-before-intelligence-book` — INPACT™ (Instant, Natural, Permitted, Adaptive, Contextual, Transparent), 7-Layer Architecture (Storage→Real-Time→Semantic→Intelligence→Governance→Observability→Orchestration), GOALS™ (Governance, Observability, Availability, Lexicon, Solid). Powers `trust/index.html`.
- **Colaberry Mermaid Diagram Design Codex** (in the Trust repo's `reference/`) — the storytelling-diagram rules in §9.5. BC: `10039770075`.
- **Enterprise Knowledge Base** — `enterprise.colaberry.ai/knowledge` — the design reference for `knowledge/index.html` (§7.18): domain tiles, one search, the "Cory" assistant, Mermaid, and downloadable one-pagers.
- **AI Project Architect repository:** `<paste repo URL>` — role taxonomy for the workforce (§6) and `src/`.
- **Accelerator curriculum (12-week / CCA-F):** `<paste doc/repo>` — real lesson names in `learning/path.html`. Building blocks: Experience Studio, Composer, the graph engine, Project Builder, Claude Code-first workflow.

> If a reference isn't provided, proceed using §9 and the concept names above; note the omission in `docs/assumptions.md`. Never block the build waiting on a reference.

---

## 16. Definition of done

The operator's browser opens to a **light**, on-brand Command Center for a company that didn't exist fifteen minutes ago. Every module clicks through to a polished, populated artifact. The website nav is the audience's own services; their tagline is the hero; their answers are highlighted throughout. The CRM pipeline drags. Mermaid diagrams tell the story. The Trust dashboard shows an 85/100 INPACT score. Numbers agree everywhere. Nothing says "coming soon."

Then the operator turns to the room:

> *"That took about twelve minutes. Our students spend twelve weeks learning to build what you just watched. This isn't the project — this is Lesson One."*
