# Program Pulse

**An AI-powered program health dashboard for program managers and chiefs of staff.**

🔗 **[Live Demo → dianaaantczak-hub.github.io/program-pulse](https://dianaaantczak-hub.github.io/program-pulse)**

---

## What it does

Program Pulse takes the inputs a PM manages every week — milestones, metrics, blockers, and stakeholders — and turns them into a live health dashboard and executive-ready outputs.

- **Auto health scoring** — calculates Red / Amber / Green status from your program data, no manual tagging
- **AI Analysis** — plain-English health explanation, top risks, recommended next action, and escalation flag
- **Exec Brief** — compact one-page summary formatted for leadership review
- **Program Report** — full MBR/QBR-ready report with metrics tables, milestone status, and risk narrative
- **Status Update** — Slack or email-ready weekly update, generated in seconds

---

## Demo presets

Three pre-loaded programs show the tool across different health states:

| Preset | Program | Status |
|---|---|---|
| 🟢 Green | Horizon Product Launch | All KPIs on track, launch in 18 days |
| 🟡 Amber | OLYSENSE AI Detection Module V2.1 | System V&V at risk, 2 open CAPAs, Q3 510(k) in jeopardy |
| 🔴 Red | NYC Office Expansion | Critical permit blocker, all KPIs off-track, move-in date at risk |

Load any preset from the **"Load Demo..."** dropdown in the top bar.

---

## Tech stack

- **Vanilla HTML / CSS / JavaScript** — no framework, no build step
- **Tailwind CSS** via CDN
- **Anthropic API** (`claude-sonnet-4-6`) for AI-generated outputs
- **localStorage** for client-side data persistence

The entire app is a single `index.html` file. Open it in a browser and it runs.

---

## How to use

**With demo data:**
1. Open the live link above
2. Select a preset from "Load Demo..." in the top bar
3. Click **Analyze with AI**, **Exec Brief**, **Program Report**, or **Status Update**

**With your own program data:**
1. Fill in the left sidebar form — program info, stakeholders, metrics, milestones, blockers
2. Click **Save Program** — data persists in your browser between sessions
3. Add your Anthropic API key in **Settings** to enable live AI outputs
4. Click any output button to generate

---

## Roadmap (V2)

- OKR integration linked to milestones and metrics
- Multi-program portfolio view with cross-program risk visibility
- Cadence-specific output templates (weekly standup, MBR, QBR)
- Health snapshots over time to surface trends
- Slack / email automation for scheduled status updates

---

