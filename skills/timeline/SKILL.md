---
name: timeline
description: Compliance project timeline and Gantt view. Visualizes all active compliance projects, accreditation cycles, regulatory deadlines, and key milestones on a text-based timeline. Shows dependencies, owner assignments, and progress. Use for quarterly planning, board presentations, and any time the VP of Compliance needs to see the full compliance roadmap.
argument-hint: "[window:quarter|6mo|year|all] [scope:projects|accreditation|regulatory|all] — e.g. 'quarter all' or 'year accreditation' or '6mo projects'"
---

# /compliance-brain:timeline — Compliance Roadmap & Timeline

You are producing a visual compliance roadmap for the VP of Compliance. The timeline answers: *What is happening, when, and in what order — and do we have the capacity to do it all?*

This is a text-based Gantt-style visualization (no graphical tools required). It combines Brain project data, accreditation cycle milestones, and regulatory deadline data into a single chronological view.

---

## Step 1: Parse the request

From the user's input, determine:

- **Window**: how far ahead to show — default to `6mo` if not specified
  - `week` — show only items due in the next 7 days
  - `month` — show only items due in the next 30 days
  - `quarter` — current quarter only (roughly 3 months)
  - `6mo` — 6-month forward view (default)
  - `year` — full 12-month view (current academic or calendar year)
  - `all` — everything with known dates regardless of how far out

- **Scope**: what to include — default to `all` if not specified
  - `projects` — active compliance projects only
  - `accreditation` — accreditation cycles and milestones only (LCME, MSCHE, ACGME, TJC)
  - `regulatory` — regulatory deadlines and submission cycles only
  - `goals` — compliance program goals with target dates only
  - `marketing` — upcoming communications and board report deadlines only
  - `all` — everything

---

## Step 2: Gather from the Brain

### Projects
- `pm/overview.md` — list of all active projects with status and phase
- `pm/index.md` — project index
- Each active project page in `pm/projects/` — read for:
  - `started` and `target_date` from frontmatter
  - Milestones listed in the Status & Timeline section
  - Risks and blockers that might affect timeline
  - Owner/lead
  - Dependencies on other projects

### Accreditation Cycles
- `wiki/compliance/` — any accreditation tracking pages
- Known cycle data from the `/compliance-brain:calendar` master deadline inventory:
  - LCME: AMER (annual), DCI (12–18 months before site visit), site visit cycle
  - MSCHE: Annual Institutional Update (July 1), PRR (year 7 or 8 of cycle), substantive change notifications
  - ACGME: Annual Program Evaluations, Annual Institutional Review, CLER visits
  - TJC: rolling survey cycle (18–36 months from last survey)

### Regulatory Deadlines
- `wiki/compliance/compliance-calendar-YYYY.md` — all tracked deadlines with due dates
- `planner/tasks.md` — deadline-related tasks with due dates

### Goals
- `planner/goals.md` — any compliance program goals with target dates

---

## Step 3: Gather live state from connectors

- **Jira**: milestone dates for active compliance projects; sprint end dates
- **Outlook calendar**: scheduled submission dates, meeting dates, board meeting dates that anchor compliance work
- **SharePoint**: accreditation portal submissions or scheduled uploads that anchor deadlines

---

## Step 4: Build the timeline data model

For each item, collect:

| Field | Description |
|-------|-------------|
| `id` | Short identifier |
| `name` | Item name |
| `type` | Project / Accreditation / Regulatory / Milestone / Goal |
| `owner` | Responsible role |
| `start` | Start date (YYYY-MM-DD or approximate month) |
| `end` | End date or due date |
| `status` | On Track 🟢 / At Risk 🟡 / Off Track 🔴 / Not Started ⚪ / Complete ✅ |
| `dependencies` | IDs of items this depends on (if known) |
| `notes` | Key milestones within the item, or blockers |

---

## Step 5: Produce the timeline

### Part A: Gantt-Style Timeline

Produce a text Gantt chart showing all items plotted across the timeline window. Use month columns.

**Format**: Each row is one item. Time is shown in month buckets. Progress is indicated with characters:

```
Symbol legend:
  ████  active period / planned duration
  ░░░░  remaining duration (if partially complete)
  ▶     milestone or single-date deadline
  ✅    completed
  🔴    overdue or at critical risk
  ⚠️    dependency or blocker present
```

```markdown
# Compliance Roadmap — [Window] View
## Generated: YYYY-MM-DD | Scope: [all/projects/accreditation/regulatory]

### Timeline: [Start Month YYYY] → [End Month YYYY]

[Table with months as columns, items as rows]

Item                              | Owner         | Jul | Aug | Sep | Oct | Nov | Dec | Jan | Feb | Mar | Apr | May | Jun |
----------------------------------|---------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
PROJECTS                          |               |     |     |     |     |     |     |     |     |     |     |     |     |
 LCME Accreditation Prep          | Dean/Comp     | ████| ████| ████| ████| ████|░░░░ |░░░░ |  ▶  |     |     |     |     |
 MSCHE Annual Institutional Update| Provost       |  ▶  |     |     |     |     |     |     |     |     |     |     |     |
 Title IX Policy Overhaul         | TIX Coord     |     | ████| ████|  ▶  |     |     |     |     |     |     |     |     |
 HIPAA Security Risk Analysis     | Privacy Off   |     |     | ████| ████|  ▶  |     |     |     |     |     |     |     |
                                  |               |     |     |     |     |     |     |     |     |     |     |     |     |
ACCREDITATION                     |               |     |     |     |     |     |     |     |     |     |     |     |     |
 ACGME Annual Program Evals       | DIO           |     | ████|  ▶  |     |     |     |     |     |     |     |     |     |
 ACGME Annual Inst Review (AIR)   | DIO/GMEC      |     |     |     | ████|  ▶  |     |     |     |     |     |     |     |
 TJC Survey Window (if applicable)| Clinical Comp |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |  ?  |
                                  |               |     |     |     |     |     |     |     |     |     |     |     |     |
REGULATORY DEADLINES              |               |     |     |     |     |     |     |     |     |     |     |     |     |
 Clery Annual Security Report     | Campus Safety |     |     |     |  ▶  |     |     |     |     |     |     |     |     |
 IPEDS Fall Survey                | IR/Registrar  |     |     |     | ████|  ▶  |     |     |     |     |     |     |     |
 OSHA 300A Posting                | HR/Facilities |     |     |     |     |     |     |  ▶  |  ▶  |  ▶  |  ▶  |     |     |
 FCOI Annual Disclosures          | Research Comp |     |     |     |     |     |     |     |     |     | ████|  ▶  |     |
 MSCHE AIU                        | Provost       |  ▶  |     |     |     |     |     |     |     |     |     |     |  ▶  |
[Continue for all items in scope]
```

**Note on the Gantt**: Adapt column widths to the window. For `quarter` mode use weeks; for `6mo` use 2-week intervals; for `year` use months; for `all` use quarters. Always show the current date with a `│NOW│` marker.

---

### Part B: Milestone List by Month

After the Gantt, produce a chronological milestone list — easier to read than the chart for specific dates:

```markdown
## Milestones & Deadlines — Chronological

### [Month YYYY]
- **[Date]** — 🔴/🟡/🟢 [Item name] — Owner: [role] — [brief note]
- **[Date]** — ▶ [Milestone] — [[pm/projects/project-name]]

### [Next Month YYYY]
...
```

---

### Part C: Capacity & Load Analysis

After the milestone list, produce a brief capacity analysis for the VP:

```markdown
## Capacity Analysis

### Peak Load Periods
The following months have the highest concentration of deadlines and project milestones:

| Month | Count | Items | Risk |
|-------|-------|-------|------|
| [Month YYYY] | N items | [Clery, MSCHE AIU, HIPAA review] | 🔴 High |
| [Month YYYY] | N items | [IPEDS, ACGME APE, policy review] | 🟠 Med |

### Dependencies & Sequencing
The following items have dependencies that could cascade if delayed:

| Item | Depends On | If Delayed Impact |
|------|-----------|-----------------|
| [LCME DCI submission] | [LCME Self-Study completion] | Site visit postponed; accreditation risk |
| [MSCHE substantive change] | [Board approval of program] | Approval delay; launch blocked |

### Staffing Gaps
Based on current project ownership, the following roles are overloaded in peak periods:
[Flag any role appearing as owner in 3+ simultaneous active items]

- [Role]: owns [N] active items in [Month] — [item1, item2, item3...]

### Recommended Sequencing
[3–5 bullets on recommended priority sequencing given load and dependencies]
1. [Start X before Y because ...]
2. [Delegate Z to ... to reduce load in October]
```

---

### Part D: Accreditation Cycle Overview (if scope includes accreditation)

```markdown
## Accreditation Cycle Status

| Accreditor | Last Action | Next Due | Cycle Stage | Prep Lead Time |
|-----------|-------------|----------|------------|----------------|
| LCME | [event — date] | [next deadline] | [stage] | 12–18 months needed |
| MSCHE | [event — date] | [next deadline — AIU Jul 1 YYYY] | [stage] | 18 months for PRR |
| ACGME | [event — date] | [next deadline] | [stage] | 6 months for CLER |
| TJC | [last survey — date] | [next expected window] | [stage] | 6 months prep |

### Accreditor Timeline Narrative
[2–3 sentences per accreditor: where we are in the cycle, what's coming, what prep is underway]
```

---

## Step 6: Offer follow-up actions

After producing output, offer:
1. **Save timeline** — write to `wiki/compliance/timelines/YYYY-MM-DD-compliance-roadmap.md`
2. **Create tasks** — add upcoming milestones as tasks in `planner/tasks.md` with due dates and owners
3. **Board presentation** — package this timeline into a board-ready format via `/compliance-brain:board-report`
4. **Load-balance** — for any overloaded roles or peak-load months, offer to run `/compliance-brain:project` on those projects for a deeper view
5. **Calendar view** — run `/compliance-brain:calendar 180` to see deadlines in the calendar format

---

## Quality Rules

- **Dates must be grounded in sources** — do not estimate or invent dates. If a deadline has no confirmed date, show it as `[TBD]` with the basis for the estimate noted (e.g., "typically October — confirm with accreditor portal").
- **Status must be explicit** — never leave a status blank. If status is unknown, say `⚠️ Status Unknown` and flag it.
- **The Gantt adapts to the window** — a 6-month view should not try to show individual days. Use the appropriate granularity for the window.
- **Capacity analysis is not optional for `full` scope** — the VP needs to know when the institution is overcommitted. A timeline without a load view is incomplete planning.
- **Dependencies are high-priority** — if Item B cannot start until Item A finishes, and A is at risk, B is automatically at risk. Surface this explicitly.
- **TJC unannounced surveys are real** — The Joint Commission's unannounced survey policy means no specific date can be shown. Mark TJC as `⚠️ Unannounced — Window: [start–end dates of expected window]` based on the last survey date and typical cycle.
