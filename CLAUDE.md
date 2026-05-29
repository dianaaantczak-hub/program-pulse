# Program Pulse — Project Context for Claude Code

## What This Is
Program Pulse is an AI-powered program health dashboard. It's a single-file web app (`index.html`) that helps program managers and chiefs of staff track milestones, metrics, blockers, and stakeholders — and automatically generates executive briefs, program reports, and status updates using the Anthropic API.

This is a portfolio project being built by Diana to demonstrate AI fluency for CoS and PM roles.

## Tech Stack
- **Single file:** Everything lives in `index.html` — HTML structure, CSS (Tailwind via CDN), and JavaScript all in one file
- **Tailwind CSS:** Loaded via CDN. Use Tailwind utility classes for all styling.
- **Vanilla JavaScript:** No frameworks. Use plain JS for all interactivity.
- **Anthropic API:** Called via fetch from the browser using the claude-sonnet-4-6 model
- **localStorage:** Used to persist program data and the API key between sessions

## Design Principles
- Clean, professional aesthetic — think Notion or Linear. White background, light gray borders, blue accent (#3B82F6)
- The layout is two-panel: left sidebar (~35% width) for the input form, right main panel (~65%) for the dashboard
- The left panel scrolls independently. The right panel is the primary view.
- Mobile is not a concern — this is a desktop demo tool

## Data Model
The app works with one program at a time. A program has:
- **Info:** name, owner, description, phase (e.g. "Q2 Execution")
- **Stakeholders:** array of {name, role}
- **Metrics/KPIs:** array of {name, current, target, status} — status is "on-track" | "at-risk" | "off-track"
- **Milestones:** array of {name, dueDate, owner, status} — status is "not-started" | "in-progress" | "complete" | "at-risk"
- **Blockers:** array of {description, severity, owner} — severity is "critical" | "medium" | "low"
- **decisionsNeeded:** string (text area)
- **openRisks:** string (text area)

All data is saved to localStorage under the key `programPulse_data` on every change.

## Health Scoring Logic (calculated in JS, before AI)
- **Red:** Any metric is off-track OR more than 1 milestone is at-risk OR unresolved critical blocker
- **Amber:** Any metric at-risk OR 1 milestone at-risk OR any critical blocker
- **Green:** Everything else

The AI layer then provides a plain-English explanation of this score.

## AI Features (Anthropic API)
All AI calls use model `claude-sonnet-4-6`. The API key is stored in localStorage under `programPulse_apiKey` and entered by the user in a settings panel.

Three AI-powered outputs:
1. **Analyze** — health explanation, top 3 risks, recommended action, escalation flag
2. **Exec Brief** — compact executive summary (~1 page), includes Goals & Metrics section
3. **Program Report** — detailed report suitable for MBR/QBR, includes full data tables and narrative
4. **Status Update** — short Slack/email format

## Output Format — Exec Brief
```
PROGRAM: [Name]
PHASE: [Phase]
STATUS: [RAG] — [one-line reason]
AS OF: [date]

SITUATION
[2-3 sentences]

GOALS & METRICS
- [Metric]: [Current] vs. target [Target] — [Status]

KEY DECISIONS NEEDED
- [item]

TOP RISKS
- [Risk 1]
- [Risk 2]
- [Risk 3]

RECOMMENDED NEXT STEPS
1. [Action]
2. [Action]
```

## Output Format — Status Update
```
[Program Name] — Week of [date]
Phase: [Phase] | Owner: [Name]
Status: [RAG emoji] [RAG label]

This week: [progress]
Next week: [planned]
Metrics: [snapshot]
Blockers: [blockers]
Decisions needed: [decisions]
```

## Demo Mode
There are 3 demo presets loadable from a dropdown:
- Green — Product Launch (Healthy)
- Amber — Platform Migration (At Risk)
- Red — Office Expansion (Critical)

These pre-fill all form fields with realistic fictional data.

## File Structure
```
program-pulse/
├── index.html     ← entire app
├── CLAUDE.md      ← this file
└── demo-data/
    ├── green.json
    ├── amber.json
    └── red.json
```

## Coding Conventions
- Keep all code in index.html. Do not create separate JS or CSS files unless specifically asked.
- Use `const` and `let`, never `var`
- Use descriptive function names (e.g. `calculateHealthScore`, `generateExecBrief`)
- Add brief comments above each major function explaining what it does
- All Anthropic API calls go through a single `callClaude(prompt)` function
- Error handling: always catch API errors and display a user-friendly message in the UI (not just console.log)

## V2 Roadmap (not building now, but design with this in mind)
- OKR integration tied to milestones and metrics
- Multi-program portfolio view
- Cadence-specific outputs (weekly, MBR, QBR templates)
- Historical health snapshots over time
- Slack/email automation
