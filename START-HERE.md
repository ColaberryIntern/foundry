# FOUNDRY — AGENT BOOTSTRAP (read this and act immediately)

**You are Claude Code, running the Colaberry AI Leadership Accelerator Open House live demo.**
The operator gave you the URL of this file. Do the steps below **in order, right now, without asking any questions.** Speed and momentum are the point — the operator is on stage.

---

## STEP 1 — Download the kit into the current folder

Run these commands (they work on Windows, macOS, and Linux — `curl` is built in):

```bash
curl -sL --create-dirs -o BusinessGenerator.md        https://raw.githubusercontent.com/ColaberryIntern/foundry/main/BusinessGenerator.md
curl -sL --create-dirs -o interview.md                https://raw.githubusercontent.com/ColaberryIntern/foundry/main/interview.md
curl -sL --create-dirs -o Interview.html              https://raw.githubusercontent.com/ColaberryIntern/foundry/main/Interview.html
curl -sL --create-dirs -o templates/command-center.html https://raw.githubusercontent.com/ColaberryIntern/foundry/main/templates/command-center.html
```

If `curl` is unavailable, use PowerShell instead:

```powershell
$b="https://raw.githubusercontent.com/ColaberryIntern/foundry/main"
New-Item -ItemType Directory -Force templates | Out-Null
"BusinessGenerator.md","interview.md","Interview.html" | % { Invoke-WebRequest "$b/$_" -OutFile $_ }
Invoke-WebRequest "$b/templates/command-center.html" -OutFile "templates/command-center.html"
```

Confirm all four files exist before continuing. If any download failed, retry that one file, then proceed.

## STEP 2 — Open the interview in the operator's browser NOW

- **Windows:** `Start-Process ".\Interview.html"`
- **macOS:** `open Interview.html`
- **Linux:** `xdg-open Interview.html`

The operator will make it full screen (F11) and fill it out live with the audience.

## STEP 3 — Stop and wait

Print exactly this and then wait — do not build anything yet:

> ✅ **The interview is open.** Fill it out with the room, click **"Copy build prompt"**, then paste the prompt back to me here and press Enter.

## STEP 4 — Build the company

When the operator pastes a prompt that contains interview answers:

1. Read `BusinessGenerator.md` (now in this folder).
2. Follow it exactly: build the entire company from the pasted answers.
3. **Do not stop** until every item in the BusinessGenerator completion checklist (§13) exists and validates. No placeholders, no dead links, no "coming soon."
4. When it validates, open `CommandCenter/index.html` in the default browser (BusinessGenerator §14).
5. Print the dramatic completion summary and the line: **"Your company is live. This is Lesson One."**

Throughout: **never ask the operator questions during the demo.** If information is missing, make a realistic assumption, record it in `docs/assumptions.md`, and keep going.

---

*One URL launches the whole show. Fill the interview → paste the prompt → watch a company get built.*
