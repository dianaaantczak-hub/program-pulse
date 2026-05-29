# Program Pulse — Build Plan & Feature Spec
*Last updated: May 14, 2026*

**What you're building:** An AI-powered program health dashboard that tracks milestones, surfaces risks, and generates executive-ready outputs. Showcase project for CoS and PM interviews.

**Output:** A single `index.html` file that opens directly in your browser. No servers, no accounts, no build step. Open it, demo it, share it.

**Interview pitch:** *"I built a program intelligence tool called Program Pulse using Claude Code and Claude's API. It takes program status data — milestones, metrics, blockers, stakeholders — and turns it into health views, executive briefs, and reports automatically. I designed it with a v2 roadmap in mind: OKR tracking, multi-program portfolio views, and cadence-specific reporting for weekly standups, MBRs, and QBRs."*

---

## Folder Structure

```
program-pulse/
├── index.html        ← the entire app (HTML + CSS + JS in one file)
├── CLAUDE.md         ← context file Claude Code reads every session
└── demo-data/
    ├── green.json    ← demo: healthy program
    ├── amber.json    ← demo: program with risks
    └── red.json      ← demo: critical program
```

Create this folder wherever makes sense on your computer (Desktop or Documents is fine).

---

## Tech Stack

- **HTML/CSS/JS** — all in one file, no framework needed
- **Tailwind CSS** — loaded via CDN, gives a clean professional look with no extra setup
- **Anthropic API** — called directly from the browser using fetch
- **localStorage** — saves your program data automatically between sessions

---

## V1 Feature Spec

### Program Input Form

| Field | Type | Notes |
|-------|------|-------|
| Program name | Text | e.g. "Platform Migration" |
| Program owner | Text | Name and/or team |
| Program description | Text area | 2-3 sentences |
| Program phase | Text | e.g. "Discovery", "Execution", "Q2 2026" |
| Stakeholders | Repeating rows | Name + role/team |
| Metrics / KPIs | Repeating rows | Metric name, current value, target, status |
| Milestones | Repeating rows | Name, due date, owner, status |
| Blockers | Repeating rows | Description, severity, owner |
| Key decisions needed | Text area | What needs resolution to move forward |
| Open risks | Text area | Known risks not yet blockers |

**Milestone statuses:** Not Started / In Progress / Complete / At Risk

**Metric statuses:** On Track / At Risk / Off Track

**Blocker severity:** Critical / Medium / Low

---

### Dashboard View

After entering data, the right panel shows:

- **Header:** Program name, owner, phase, RAG badge, last saved timestamp
- **Health score:** Red / Amber / Green + one-line AI reason
- **Metrics panel:** Table — metric, current, target, status chip
- **Milestone tracker:** List with status chips + due dates, progress bar at top
- **Blockers panel:** Grouped by severity, critical ones highlighted
- **Stakeholders panel:** Name and role list
- **AI Analysis panel:** Health explanation, top 3 risks, recommended action, escalation flag
- **Action buttons:** Generate Exec Brief | Generate Program Report | Generate Status Update

**Auto health scoring logic:**
- Green: Milestones on track, metrics on track, no critical blockers
- Amber: 1-2 milestones at risk OR any metric at risk OR 1 critical blocker
- Red: Multiple milestones at risk, metrics off track, or unresolved critical blockers

---

### Exec Brief (compact, for executives)

```
PROGRAM: [Name]
PHASE: [Phase]
STATUS: [RAG] — [one-line reason]
AS OF: [date]

SITUATION
[2-3 sentences on what this program is and where it stands]

GOALS & METRICS
- [Metric]: [Current] vs. target [Target] — [Status]

KEY DECISIONS NEEDED
- [Decision]

TOP RISKS
- [Risk 1]
- [Risk 2]
- [Risk 3]

RECOMMENDED NEXT STEPS
1. [Action]
2. [Action]
```

---

### Program Report (detailed, for MBRs and reviews)

Longer format with narrative sections and full data tables. Includes everything in the exec brief plus:
- 3-5 sentence program overview narrative
- Full milestone status table
- Full metrics table with notes
- Risk analysis with mitigations
- Decisions log

---

### Status Update (for Slack or email)

```
[Program Name] — Week of [date]
Phase: [Phase] | Owner: [Name]
Status: [RAG emoji] [RAG label]

This week: [milestones hit / progress made]
Next week: [what's planned]
Metrics: [one-line snapshot]
Blockers: [what's in the way]
Decisions needed: [from stakeholders]
```

---

### Demo Mode

A "Load Demo" dropdown with 3 presets at different health states — Green, Amber, Red. Pre-fills all fields with a realistic fictional program. This is what you use in interviews.

---

## V2 Roadmap

- **OKR integration** — link milestones and metrics to team OKRs
- **Multi-program portfolio** — track 3-5 programs, see cross-program risks
- **Cadence templates** — one-click MBR deck, QBR summary, weekly digest
- **Health history** — snapshot health over time, see trends
- **Slack/email automation** — scheduled status pushes

---

## Daily Build Plan

**12 hours across 4 days. Today is Day 1.**

---

### May 14 (TODAY) — Setup + App Shell + Input Form (3 hrs)

*Goal: Program Pulse opens in your browser, the input form works, and the dashboard shows a placeholder layout.*

**Step 1: Set up your project (15 min)**

1. Create folder: `program-pulse` (on Desktop or Documents)
2. Copy `CLAUDE.md` into it (see separate file)
3. Open your terminal and navigate to the folder:
   ```
   cd ~/Desktop/program-pulse
   ```
4. Start Claude Code:
   ```
   claude
   ```
5. Claude Code will read your CLAUDE.md automatically and know what you're building.

**Step 2: Scaffold the app (45 min)**

Paste this as your first message in Claude Code:

> "I'm starting a new project called Program Pulse. Read the CLAUDE.md for full context. Start by creating index.html — a single-file web app with Tailwind CSS loaded via CDN. Build a two-panel layout: a left sidebar (about 35% width) for the program input form, and a right main panel (65%) for the health dashboard. The left panel should have a scrollable form. The right panel should show placeholder cards for: health badge, metrics, milestones, blockers, stakeholders, AI analysis, and action buttons. Use a white background with light gray borders, blue accent (#3B82F6), and clean sans-serif typography."

**Step 3: Build the input form (1 hr)**

Once the layout is in, ask Claude Code to build each form section:

> "Build the full input form in the left sidebar. Sections: (1) Program Info — name, owner, description, phase. (2) Stakeholders — repeating rows of name + role with an Add button. (3) Metrics/KPIs — repeating rows of metric name, current value, target value, status dropdown (On Track / At Risk / Off Track). (4) Milestones — repeating rows of name, due date, owner, status dropdown (Not Started / In Progress / Complete / At Risk). (5) Blockers — repeating rows of description, severity dropdown (Critical / Medium / Low), owner. (6) Text areas for Key Decisions Needed and Open Risks. Add a Save button at the bottom that saves to localStorage."

**Step 4: Wire up localStorage (30 min)**

> "Add auto-save: whenever any field changes, save the full form state to localStorage under the key 'programPulse_data'. On page load, restore from localStorage if data exists. Add a visible 'Last saved: [time]' indicator near the Save button."

**End goal:** You can fill in the form, refresh the page, and your data is still there.

---

### May 18 (Sunday) — AI Analysis + Dashboard Panels (3 hrs)

*Goal: The dashboard reads real form data and Claude analyzes it.*

**First hour — wire form to dashboard:**
> "Now make the dashboard panels dynamic. When the form data changes, update the dashboard: show the list of stakeholders, show milestones with colored status chips (green=Complete, blue=In Progress, gray=Not Started, red=At Risk), show metrics with status chips, show blockers grouped by severity with critical ones in a red highlight box."

**Second hour — health scoring:**
> "Add automatic health scoring. Calculate the RAG status based on this logic: Red if any metric is Off Track OR more than 1 milestone is At Risk OR there are unresolved Critical blockers. Amber if any metric is At Risk OR 1 milestone is At Risk OR any Critical blocker exists. Green otherwise. Show the RAG badge prominently at the top of the dashboard with the label and appropriate color."

**Third hour — AI analysis:**
- Get your Anthropic API key at console.anthropic.com (free tier is enough)
- Add an API key field to the app settings (stored in localStorage, never sent anywhere except Anthropic)

> "Add an 'Analyze with AI' button. When clicked, it takes all the form data, formats it into a structured prompt, and sends it to the Anthropic API (model: claude-sonnet-4-6). Display the result in the AI Analysis panel with 4 sections: (1) health explanation in plain English, (2) top 3 risks ranked by impact, (3) one recommended next action, (4) a yes/no escalation flag with a one-sentence reason. Show a spinner while loading. Handle API errors gracefully."

---

### May 19 (Monday) — Output Generators (2 hrs)

*Goal: All three outputs work — exec brief, program report, status update.*

**First hour:**
> "Add a 'Generate Exec Brief' button. When clicked, call the Anthropic API with all program data and generate an exec brief in this exact format: [paste the exec brief template from the spec]. Display it in a modal with a copy-to-clipboard button and a download as .txt button."

> "Add a 'Generate Status Update' button that produces the shorter Slack/email format. Same modal with copy and download."

**Second hour:**
> "Add a 'Generate Program Report' button that produces a detailed report with: program overview narrative (3-5 sentences), full metrics table, full milestone table, blocker and risk summary with mitigations, stakeholder list, and AI analysis section. Same modal with copy and download."

Then build the demo programs:
> "Add a 'Load Demo' dropdown with 3 options: 'Green — Product Launch (Healthy)', 'Amber — Platform Migration (At Risk)', 'Red — Office Expansion (Critical)'. Each option pre-fills all form fields with realistic fictional data that reflects its health state. Clearing the form resets to blank."

---

### May 20 (Tuesday) — Polish + Demo Prep (2 hrs)

*Goal: App looks sharp and you can demo it confidently.*

**First hour — polish:**
> "Do a full styling pass. Make the app look polished and professional. Improve: (1) visual hierarchy — program name and health badge should be prominent, (2) the metrics and milestone tables should be clean and scannable, (3) the action buttons should be prominent and well-spaced, (4) the AI Analysis panel should feel distinct — maybe a light blue background. Fix any layout issues."

**Second hour — demo prep:**
- Practice the 3-minute demo: open app, explain it, load Amber demo, click Analyze, generate exec brief
- Write your 3 interview talking points (see below)
- Optional: add a second program to show switching between programs

**Your 3 interview talking points:**

1. *What you built:* "Program Pulse is an AI-powered program health tool. You enter your milestones, metrics, blockers, and stakeholders, and it automatically scores program health and generates executive-ready outputs. I built it with Claude Code in about 12 hours across a week."

2. *What you learned:* "I learned how to use Claude Code to iterate on a real product — I'd describe a feature, review what it built, and refine through conversation. I also learned how to prompt an AI model to produce reliable structured outputs, not just freeform text."

3. *What's next:* "The v2 roadmap includes OKR integration, a multi-program portfolio view, and cadence-specific outputs for MBRs and QBRs. The architecture supports all of that — it was designed with extensibility in mind."

---

## Claude Code Tips

**Start every session by saying:**
> "I'm working on Program Pulse. Read CLAUDE.md for context. Here's where I left off: [one sentence]. Today I want to [goal]."

**The iteration loop:**
1. Ask for a feature
2. Refresh `index.html` in your browser
3. Tell Claude Code what to adjust
4. Repeat

**When something breaks:**
> "This isn't working — [describe]. Here's the browser console error: [paste]. Fix it."

**When you want to understand something:**
> "Explain what this part of the code does in plain English, like I'm a smart non-developer."

**When the UI looks off:**
> "The [element] looks crowded / too small / misaligned. [Describe what you want instead]."
