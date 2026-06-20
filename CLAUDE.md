# HE Compliance Brain — Claude Code Plugin

A Claude Code plugin providing a second brain / PKM system and full compliance toolkit for the VP of Compliance at a higher education institution (medical school / research university). Zero dependencies — pure markdown skill files that leverage Claude's built-in tools.

## Plugin Structure

```
he-compliance-brain/
  .claude-plugin/
    plugin.json          — plugin manifest (name: compliance-brain)
  skills/
    <name>/
      SKILL.md           — skill instruction file (one per command)
  CLAUDE.md              — this file
```

Each `skills/<name>/SKILL.md` becomes `/compliance-brain:<name>` in Claude Code when the plugin is installed.

## How Skills Work

Skills are instruction sets Claude follows when a slash command is invoked. No Python, no server, no dependencies. Claude uses its built-in tools:
- `Read`, `Write`, `Edit` — file operations on Brain pages
- `Grep`, `Glob` — search the Brain
- `WebFetch` — fetch regulatory agency websites and accreditor pages
- MCP connectors — Jira, Outlook calendar, Outlook email, Teams, SharePoint (when available in the user's Claude Code environment)

## The Brain Directory Structure

Skills operate on a "Brain" directory — a structured knowledge store the user owns. Default location is configured at bootstrap via `/compliance-brain:newbrain`.

```
<brain-root>/
  CLAUDE.md           — Brain schema and navigation instructions
  templates.md        — Page templates for all Brain page types
  log.md              — Operational changelog (Brain mutations only)
  wiki/
    index.md          — Wiki index
    overview.md       — Wiki narrative overview
    concepts/         — Knowledge: regulatory concepts, frameworks, doctrine
    entities/         — People, organizations, institutions
    compliance/       — Compliance documents: risk register, training register, calendars
      risk-register.md
      training-register.md
      compliance-calendar-YYYY.md
      reg-monitor/    — Regulatory intelligence briefs
      dashboards/     — Saved dashboard snapshots
      timelines/      — Saved timeline/roadmap views
  pm/
    index.md          — PM index
    overview.md       — Active project narrative
    projects/         — Project pages (one per initiative)
    meetings/         — Meeting pages (one per meeting)
    notes/            — Freeform PM notes
    prep/             — Pre-meeting briefs
    reports/          — Audit reports, board reports, risk reports
  planner/
    tasks.md          — Active task list (all projects)
    goals.md          — Compliance program goals
    dashboard.md      — Current priorities snapshot
    index.md          — Planner index
    YYYY/
      MM/
        YYYY-MM-DD.md — Daily planner files
        week-WW.md    — Weekly reflection files
  investigations/
    index.md          — Case register (all active and closed matters)
    overview.md       — Investigation program summary
    active/           — Active compliance matter case files (INV-NNN.md)
    closed/YYYY/      — Archived closed matters
  evidence/
    index.md          — Master evidence catalog
    overview.md       — Evidence locker status summary
    audits/           — Assembled audit-specific evidence packages
  counsel/
    index.md          — Legal library index
    overview.md       — Current legal landscape
    memos/            — Legal memoranda
    opinions/         — Regulatory interpretations, AG opinions
    guidance/         — Regulatory guidance analyses
    matters/          — Active and closed external legal matters
    agreements/       — Resolution agreements, consent orders
    templates/        — Standard agreement templates
  intel/
    index.md          — Intelligence library index (newest first)
    overview.md       — Current intelligence landscape
    enforcement/      — Enforcement actions at peer institutions
    regulatory/       — Regulatory developments
    peer/             — Peer institution news and compliance failures
  raw/
    *.ref.md          — Connector-reference stubs ONLY (see Data Governance below)
```

## Data Governance — CRITICAL

**Outlook emails, Teams chats, and Teams meeting transcripts must NEVER be stored verbatim in `raw/` or any Brain file.** This is a hard data governance rule.

Only **connector-reference stubs** (`.ref.md` files with `type: connector-reference` frontmatter) are stored in `raw/`. These contain only metadata and retrieval instructions — no verbatim message body content.

Knowledge derived from these sources (summaries, decisions, action items, analysis) is captured in proper Brain pages (meeting pages, notes, wiki concepts).

The `/compliance-brain:lint` skill enforces this rule and will flag violations.

---

## Skill Reference

### Core Brain Operations

| Command | Description |
|---------|-------------|
| `/compliance-brain:newbrain` | Bootstrap a new Brain — guided setup wizard that creates the full directory structure, CLAUDE.md schema, templates, and initial index files |
| `/compliance-brain:myday` | Daily briefing — sync connector state, surface reminders and deadlines, present today's plan. Mon: full sync + lint + plot. Tue–Thu: sync. Fri: sync + reflect |
| `/compliance-brain:ask` | Query the Brain — top-down tree search with citations; best for "what do we know about X?" |
| `/compliance-brain:ingest` | Source intake — process documents, transcripts, readings, URLs into proper Brain pages with connector-reference stubs |
| `/compliance-brain:log` | Activity logging — append timestamped entry to today's daily file from conversation context |
| `/compliance-brain:reflect` | End-of-day or week reflection — synthesize daily logs, prune tasks, promote insights to wiki |
| `/compliance-brain:standup` | 3-part standup generator: Yesterday / Today / Blockers |
| `/compliance-brain:sync` | Sync Brain project knowledge with live connector state (Jira, Teams, SharePoint) |
| `/compliance-brain:lint` | Brain health check — finds schema drift, orphan pages, broken links, stale content, raw governance violations |
| `/compliance-brain:plot` | Weekly planning — creates Mon–Fri daily planner files with tasks and priorities |

### Project Management

| Command | Description |
|---------|-------------|
| `/compliance-brain:project` | View, create, or list projects. View: unified briefing with live connector drift detection. Create: scaffold project page, entity pages, PM index entries |
| `/compliance-brain:met` | Meeting transcript acquisition — fetches from Teams connector, creates meeting page |
| `/compliance-brain:prep` | Pre-meeting brief — pulls project state, entity context, prior meetings, open questions |
| `/compliance-brain:ticket` | Draft a Jira ticket grounded in Brain context. Always presents draft for approval before creating |
| `/compliance-brain:compose` | Draft a message (email, Teams, Jira comment) grounded in Brain context. Always presents draft for approval before sending |

### Planning & Visualization

| Command | Description |
|---------|-------------|
| `/compliance-brain:dashboard` | Compliance program dashboard — single-pane view of risk posture, deadlines, project status, training, audit standing. Modes: full, quick, risks, calendar, projects, training |
| `/compliance-brain:timeline` | Compliance roadmap & Gantt view — visualizes projects, accreditation cycles, regulatory deadlines on a text timeline with capacity analysis. Modes: quarter, 6mo, year, all |
| `/compliance-brain:calendar` | Compliance deadline calendar — all regulatory reporting deadlines, accreditation milestones, certification cycles. Modes: calendar, overdue, quarter, annual |
| `/compliance-brain:remind` | Deadline reminder management — creates reminder task chains in the planner, surfaces alert digests. Modes: check, set, digest, clear |

### Confidential Sub-Brain Skills

| Command | Description |
|---------|-------------|
| `/compliance-brain:investigate` | Compliance investigation and case management — Title IX, research misconduct, HIPAA breaches, employee complaints, self-disclosures. Maintains confidential case register with required process deadlines and regulatory timelines. Modes: new, update, close, review, report |
| `/compliance-brain:evidence` | Compliance evidence locker — catalogs where audit artifacts live, what they prove, and whether they're sufficient. Produces audit evidence packages and gap analyses. Modes: catalog, collect, package, gap |
| `/compliance-brain:counsel` | Legal research library — files and retrieves legal memos, regulatory interpretations, resolution agreements, outside counsel correspondence. Manages external legal matters (OCR complaints, DOJ inquiries). Modes: file, search, brief, index, matter |
| `/compliance-brain:intel` | Regulatory and peer intelligence feed — curated clipping library of enforcement actions, regulatory developments, and peer institution news. Produces pattern-based alerts and weekly digests. Modes: file, search, feed, alert, digest |

### Proactive Intelligence

| Command | Description |
|---------|-------------|
| `/compliance-brain:scan` | Proactive weekly gap scan — sweeps all domains, surfaces only what is new or worsening since last scan, produces a ranked priority list with quick wins. Runs automatically on Mondays via myday |
| `/compliance-brain:delta` | Change detection — compares current Brain state against prior scan snapshots to show what moved (risks up/down, deadlines slipped, projects changed status). Modes: compare, trend, snapshot |

### Compliance Workflows

| Command | Description |
|---------|-------------|
| `/compliance-brain:compliance` | General regulatory compliance research — brief, gap, remediate, wiki modes |
| `/compliance-brain:risk` | Compliance risk register — build, rate (with effort scoring), treat, and report. Priority index (🔥 Act Now / ⚡ Quick Win / 📋 Plan / ⏳ Defer) derived from severity × effort. Modes: register, update, rate, treat, report, heat-map, prioritize |
| `/compliance-brain:reg-monitor` | Regulatory intelligence — scan, brief, action, horizon modes. Fetches from authoritative agency sources |
| `/compliance-brain:audit` | External audit response — corrective action plans, status tracking, escalation, board brief |
| `/compliance-brain:policy` | Policy registry — inventory, gaps, overdue policies, policy maps, draft new policies |
| `/compliance-brain:board-report` | Board and compliance committee reporting — full, brief, risk-only, audit-only, quarter modes |
| `/compliance-brain:training` | Mandatory training tracker — completion rates, gaps, overdue populations, certification cycles |
| `/compliance-brain:review` | Compliance collateral review — quick, full, redline modes for reviewing documents against requirements |

### Domain-Specific Skills

| Command | Description |
|---------|-------------|
| `/compliance-brain:titleix` | Title IX compliance — gap analysis, policy review, coordinator support |
| `/compliance-brain:clery` | Clery Act compliance — ASR preparation, crime log review, geography analysis |
| `/compliance-brain:coi` | COI/FCOI management — disclosure tracking, management plans, retrospective reviews |
| `/compliance-brain:research` | Research compliance — IRB, IACUC, IBC, export controls, misconduct, sponsored programs |
| `/compliance-brain:acgme` | ACGME GME compliance — CLER prep, APE review, GMEC documentation |
| `/compliance-brain:lcme` | LCME accreditation — gap analysis, DCI support, AFI tracking |
| `/compliance-brain:msche` | MSCHE accreditation — AIU preparation, PRR support, substantive change |
| `/compliance-brain:substantive-change` | Substantive change assessment — MSCHE, LCME, SACSCOC notification requirements |

---

## Skill Invocation Chains

Some skills call others in sequence:

- **`/compliance-brain:myday`** calls `sync` (daily), `scan quick` (Monday), `lint` (Monday), `plot` (Monday), `reflect` (Friday), and `remind digest` (daily)
- **`/compliance-brain:dashboard`** delegates to `risk`, `calendar`, `training`, and `project` for focused modes
- **`/compliance-brain:board-report`** aggregates output from `risk`, `reg-monitor`, `audit`, `training`, and `calendar`
- **`/compliance-brain:risk`** sources risks from all domain skills run in `gap` mode

---

## Evidence Standards

Every factual claim in a compliance output must cite a specific regulatory provision, accreditation standard, or policy document. The format is:

> *[Claim]. [Regulation/Standard], [Section/Citation].*

Skills never manufacture regulatory citations. If a citation cannot be confirmed, the output flags the claim as unverified.

---

## Plugin Version

`compliance-brain` v1.0.0
