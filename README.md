# HE Compliance Brain

A Claude Code plugin that gives the VP of Compliance at a higher education institution a complete second brain and compliance toolkit — built entirely from markdown skill files, with no Python, no server, and no dependencies.

It installs as a Claude Code plugin. Every skill becomes a `/compliance-brain:<name>` slash command. Claude does the work using its built-in tools (Read, Write, Grep, Glob, WebFetch) and whatever MCP connectors you have configured (Jira, Outlook, Teams, SharePoint).

---

## What It Does

**Second brain / PKM** — Capture meetings, decisions, readings, and people. Query knowledge with citations. Reflect, synthesize, and plan.

**Compliance program management** — Risk register, regulatory monitoring, audit response, policy tracking, training compliance, board reporting — all grounded in your Brain's institutional knowledge.

**Domain-specific compliance** — Title IX, Clery Act, FCOI/COI, research compliance (IRB, IACUC, IBC, export controls), ACGME GME, LCME, MSCHE accreditation, substantive change.

**Confidential sub-brains** — Investigations case management, audit evidence locker, legal reference library, regulatory intelligence feed.

**Planning and visualization** — Compliance program dashboard, Gantt-style roadmap, compliance deadline calendar, proactive reminder chains.

---

## Requirements

- [Claude Code](https://claude.ai/code) (desktop app, CLI, or IDE extension)
- Claude Code plugin support enabled
- Optional but recommended: MCP connectors for Microsoft 365 (Outlook, Teams, SharePoint) and/or Atlassian (Jira, Confluence)

---

## Installation

### 1. Install the plugin

From your terminal:

```bash
claude plugin install he-compliance-brain
```

Or, if installing from a local clone of this repo:

```bash
git clone https://github.com/nantasket-ai/he-compliance-brain
claude plugin install ./he-compliance-brain
```

Verify the plugin is installed:

```bash
claude plugin list
```

You should see `compliance-brain` in the list.

### 2. Bootstrap your Brain

The Brain is a directory on your filesystem where all your knowledge, projects, plans, and compliance records live. Run the bootstrap wizard once to set it up:

```
/compliance-brain:newbrain ~/my-compliance-brain
```

Replace `~/my-compliance-brain` with any path you want. The wizard will:

- Create the full directory structure (wiki, pm, planner, investigations, evidence, counsel, intel, raw)
- Install the Brain schema (`CLAUDE.md`) and page templates
- Ask about your timezone, MCP connectors, and external systems (Jira project keys, etc.)
- Configure the `brain_path` plugin setting so skills find your Brain from any directory

The wizard takes about 2 minutes. Answer its questions and it handles everything else.

### 3. Start your first day

```
/compliance-brain:myday
```

This is your morning command. It syncs connector state, surfaces deadline reminders, and presents today's plan. On Mondays it also runs a Brain health check and plots your full week.

---

## Directory Structure Created by newbrain

```
<brain-root>/
  CLAUDE.md                    ← Brain schema and operating manual
  templates.md                 ← Page templates for all page types
  log.md                       ← Operational changelog
  wiki/
    concepts/                  ← Regulatory frameworks, doctrine, concepts
    entities/                  ← People, organizations, institutions
    compliance/
      risk-register.md         ← Compliance risk register
      training-register.md     ← Training compliance tracker
      compliance-calendar-YYYY.md
      reg-monitor/             ← Regulatory intelligence briefs
      dashboards/              ← Saved dashboard snapshots
      timelines/               ← Saved roadmap views
  pm/
    projects/                  ← Compliance initiative project pages
    meetings/                  ← Meeting pages (decisions, action items)
    notes/                     ← Freeform PM notes
    prep/                      ← Pre-meeting briefs
    reports/                   ← Audit reports, board reports
  planner/
    tasks.md                   ← Active task list
    goals.md                   ← Compliance program goals
    YYYY/MM/YYYY-MM-DD.md      ← Daily planner files
  investigations/
    active/                    ← Active compliance matter case files
    closed/YYYY/               ← Archived closed matters
  evidence/
    audits/                    ← Assembled audit evidence packages
  counsel/
    memos/                     ← Legal memoranda
    opinions/                  ← Regulatory interpretations, AG opinions
    guidance/                  ← Regulatory guidance analyses
    matters/                   ← Active external legal matters
    agreements/                ← Resolution agreements, consent orders
  intel/
    enforcement/               ← Enforcement actions at peer institutions
    regulatory/                ← Regulatory developments
    peer/                      ← Peer institution news
  raw/
    *.ref.md                   ← Connector-reference stubs only
```

---

## Skill Reference

### Core Brain Operations

| Command | What It Does |
|---------|-------------|
| `/compliance-brain:newbrain` | Bootstrap wizard — creates Brain directory structure, installs schema, configures timezone and connectors |
| `/compliance-brain:myday` | Morning briefing — syncs connectors, surfaces reminders, presents today's plan |
| `/compliance-brain:ask` | Query the Brain — top-down search with claim-level citations |
| `/compliance-brain:ingest` | File a source (document, URL, notes) into the Brain |
| `/compliance-brain:log` | Append an activity log entry to today's daily file |
| `/compliance-brain:reflect` | End-of-day or week reflection — synthesize activity, prune tasks, promote insights |
| `/compliance-brain:standup` | Generate a 3-part standup: Yesterday / Today / Blockers |
| `/compliance-brain:sync` | Sync Brain project knowledge with live connector state |
| `/compliance-brain:lint` | Brain health check — orphan pages, broken links, stale content, governance violations |
| `/compliance-brain:plot` | Weekly planning — create Mon–Fri daily planner files |

### Project Management

| Command | What It Does |
|---------|-------------|
| `/compliance-brain:project` | View, create, or list compliance projects with live connector drift detection |
| `/compliance-brain:met` | Fetch a Teams meeting transcript and process it into a meeting page |
| `/compliance-brain:prep` | Generate a pre-meeting brief from Brain context and live connector data |
| `/compliance-brain:ticket` | Draft a Jira ticket grounded in Brain context (shows draft before creating) |
| `/compliance-brain:compose` | Draft a message (email, Teams, Jira comment) from Brain context (shows draft before sending) |

### Planning & Visualization

| Command | What It Does |
|---------|-------------|
| `/compliance-brain:dashboard` | Compliance program dashboard — risk, deadlines, projects, training, investigations, evidence |
| `/compliance-brain:timeline` | Gantt-style compliance roadmap — projects, accreditation cycles, regulatory deadlines with capacity analysis |
| `/compliance-brain:calendar` | Compliance deadline calendar — all regulatory and accreditation deadlines |
| `/compliance-brain:remind` | Deadline reminder chains — tiered reminders (90/60/30/14/7/1-day) filed into the planner |

### Compliance Workflows

| Command | What It Does |
|---------|-------------|
| `/compliance-brain:compliance` | General regulatory compliance research and gap analysis |
| `/compliance-brain:risk` | Compliance risk register — build, rate, treat, and report |
| `/compliance-brain:reg-monitor` | Regulatory intelligence — scan agency websites for new rules, guidance, enforcement actions |
| `/compliance-brain:audit` | External audit response — corrective action plans, status tracking, escalation |
| `/compliance-brain:policy` | Policy registry — inventory, gaps, overdue policies, draft new policies |
| `/compliance-brain:board-report` | Board and compliance committee reporting |
| `/compliance-brain:training` | Mandatory training tracker — completion rates, gaps, overdue populations |
| `/compliance-brain:review` | Compliance document review against regulatory requirements |

### Confidential Sub-Brain Skills

| Command | What It Does |
|---------|-------------|
| `/compliance-brain:investigate` | Compliance investigation management — Title IX, research misconduct, HIPAA breaches, employee complaints, self-disclosures. Required federal process timelines pre-loaded. |
| `/compliance-brain:evidence` | Compliance evidence locker — catalog where audit artifacts live, assess sufficiency, package for auditors |
| `/compliance-brain:counsel` | Legal reference library — file and retrieve legal memos, regulatory interpretations, resolution agreements, outside counsel correspondence |
| `/compliance-brain:intel` | Regulatory and peer intelligence — capture and pattern-track enforcement actions, peer institution news, regulatory developments |

### Domain-Specific Skills

| Command | What It Does |
|---------|-------------|
| `/compliance-brain:titleix` | Title IX compliance — gap analysis, policy review, coordinator support |
| `/compliance-brain:clery` | Clery Act compliance — ASR preparation, crime log review |
| `/compliance-brain:coi` | COI/FCOI management — disclosure tracking, management plans |
| `/compliance-brain:research` | Research compliance — IRB, IACUC, IBC, export controls, misconduct, sponsored programs |
| `/compliance-brain:acgme` | ACGME GME compliance — CLER prep, APE review, GMEC documentation |
| `/compliance-brain:lcme` | LCME accreditation — gap analysis, DCI support, AFI tracking |
| `/compliance-brain:msche` | MSCHE accreditation — AIU preparation, PRR support, substantive change |
| `/compliance-brain:substantive-change` | Substantive change assessment — MSCHE, LCME, SACSCOC notification requirements |

---

## Recommended Starting Workflow

**Week 1 — Set up the foundations:**

1. Run `/compliance-brain:newbrain` to create your Brain
2. Run `/compliance-brain:risk all register` to start building the risk register
3. Run `/compliance-brain:calendar all annual` to see all compliance deadlines for the year
4. Run `/compliance-brain:remind set all` to create reminder chains for every deadline
5. Run `/compliance-brain:dashboard full` to see your starting compliance program health

**Week 2 — Start capturing institutional knowledge:**

6. For each active compliance project: `/compliance-brain:project new <name>`
7. Ingest prior audit reports: `/compliance-brain:ingest` (paste or provide file path)
8. Run `/compliance-brain:policy inventory` to assess the policy registry
9. Run `/compliance-brain:training` to assess current training compliance

**Ongoing — Daily and weekly habits:**

- Every morning: `/compliance-brain:myday`
- After every significant meeting: `/compliance-brain:met` or `/compliance-brain:log`
- Before every board meeting: `/compliance-brain:board-report full`
- Weekly: `/compliance-brain:reg-monitor all scan` to stay current on the regulatory horizon
- Monthly: `/compliance-brain:dashboard full` and `/compliance-brain:risk all register`

---

## MCP Connectors

The plugin works without connectors but is significantly more powerful with them. When connectors are configured, skills pull live data from Jira, Outlook, Teams, and SharePoint rather than relying solely on what's in the Brain.

**Microsoft 365** (Outlook, Teams, SharePoint): Configure in Claude Code Settings → Integrations. Covers calendar events, email search, Teams transcripts, and SharePoint document search in one connection.

**Atlassian** (Jira, Confluence): Configure in Claude Code Settings → Integrations. Enables ticket creation and updates, JQL search, and Confluence page retrieval.

If you're unsure what's connected, run `/compliance-brain:newbrain` — the setup wizard will test your connectors and report what's available.

---

## Data Governance

**Outlook emails, Teams chats, and Teams meeting transcripts are never stored verbatim in the Brain.** This is a hard data governance rule enforced by the plugin and checked by `/compliance-brain:lint`.

Instead, connector-sourced content is:
1. Processed in-context to extract decisions, action items, and summaries
2. Filed as derived Brain pages (meeting pages, notes)
3. Referenced via a `.ref.md` connector-reference stub in `raw/` — containing only retrieval metadata, never message body content

This ensures the Brain doesn't become a parallel archive that outlives the source system's retention policy.

---

## Confidentiality Notes

- **`investigations/`** pages contain sensitive compliance matter information. They are never cross-referenced by case detail from wiki or pm pages. Dashboard references to "N active matters" are acceptable; full case details stay in `investigations/`.
- **`counsel/`** pages may contain attorney-client privileged material. Privilege is tagged per document. Privileged content is never included in board reports or shared-facing summaries.
- The Brain lives entirely on your filesystem (or wherever you put it). Nothing is sent to external services except through your explicitly configured MCP connectors.

---

## About

Built by [Nantasket AI](https://nantasket.ai) for compliance professionals at research universities and academic medical centers.

Plugin version: `compliance-brain` v1.0.0
