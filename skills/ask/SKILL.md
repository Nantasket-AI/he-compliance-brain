---
name: ask
description: Query the Brain's knowledge. Searches across all sub-brains and connectors to answer questions with cited sources. Use for any question about stored knowledge, projects, meetings, or concepts.
argument-hint: <question>
---

# /the-brain:ask — Query the Brain

Answer a question by synthesizing the Brain's accumulated knowledge with live connector data. Every claim in the answer must be traceable to a specific source.

## Step 1: Understand the question

Parse the user's question. Determine:
- **Which sub-brains are relevant**:
  - General knowledge (what is X, how does Y work) → Scholar (`wiki/`)
  - Project/business (what did we decide, what's the status, who's involved) → PM (`pm/`)
  - Operational (what's on my plate, what's next, when is the meeting) → Planner (`planner/`)
  - Cross-cutting → multiple sub-brains
- **Whether live data is needed**: if the question involves current state (ticket status, upcoming meetings, recent messages), plan to query connectors in Step 3.
- **Scope**: is this a narrow factual lookup, a broad synthesis, or an analysis requiring judgment?

## Step 2: Navigate the Brain (top-down tree search)

Follow the CLAUDE.md navigation sequence. Navigate like a tree search — top-down, skipping irrelevant branches. **Never scan exhaustively.**

1. Read `overview.md` for each potentially relevant sub-brain — decide which brain(s) are relevant, skip the rest entirely
2. Read the relevant brain's `index.md` — use category/project rollup summaries to identify the right branch
3. Read category or project rollup summaries first — these may already answer the question or narrow the search
4. Drill into individual pages only within the identified branch
5. For project questions, go straight to `pm/index.md` → find the project section (which groups project page, meetings, and notes) → read the project page first, then meetings only if needed
6. For entity/concept questions, check `wiki/index.md` → entity or concept section → specific page

**Key principle**: Read the minimum number of pages needed to answer confidently. The overviews and index rollups exist to prevent exhaustive scanning.

## Step 3: Gather evidence from the Brain

Read the specific pages identified in Step 2. For each relevant fact:
- Note the **exact claim** and the specific section it comes from
- Note the **source chain**: `[[page#heading]]` — this is what goes in the answer
- Note whether the claim has a raw source trail (frontmatter `raw_source` or inline `Source: [[raw/...]]`). Note: `.ref.md` connector-reference stubs (type: `connector-reference`) are valid raw sources — they contain metadata and retrieval instructions for emails, Teams messages, and transcripts rather than verbatim content.
- Note the **freshness** — when was the page last updated? Is this potentially stale?

**Check for contradictions**: if multiple pages claim different things about the same fact, note both versions and their sources. Use the CLAUDE.md contradiction handling convention (`> [!conflict]` callout).

## Step 4: Gather live state from connectors (if needed)

For questions about current state, augment Brain knowledge with connector data:

- **Jira**: current ticket status, sprint state, recent updates — use JQL with the project's `jira_project` key from the project page
- **Outlook calendar**: upcoming meetings, schedule queries
- **Outlook email**: recent communications about a topic or from a person
- **Teams**: recent messages in project group chats (check project page Live Context for chat IDs)
- **SharePoint**: documents related to the query
- **Confluence**: living docs referenced in project pages (check References sections for page IDs)

When connector data is used, note the source explicitly (e.g., "per Jira as of today", "from Outlook calendar") so the user knows what's from the Brain vs. what's live.

## Step 5: Synthesize the answer

Combine Brain knowledge and connector data into a coherent answer:

- **Every factual claim includes a clickable `[[page#heading]]` citation** — at the fact level, not the document level
- **Connector-sourced facts** are marked with their source (e.g., "per Jira", "from calendar")
- **Contradictions** are flagged explicitly with both versions and sources — don't silently pick one
- **Gaps** are flagged — things the Brain doesn't know that would improve the answer. Offer to research further or create a page.
- **Confidence level** is implicit in the citation density — well-sourced claims have links, uncertain claims are flagged

Structure the answer based on the question type:
- **Factual lookup**: direct answer with citation, one or two sentences
- **Status/state query**: structured summary with current state, recent changes, and what's next
- **Analysis/comparison**: organized sections with evidence for each point
- **Cross-cutting**: answer organized by sub-brain, with cross-references between them

## Step 6: Offer to file

If the answer is substantive — a useful analysis, comparison, synthesis, or research result that would be valuable to have on file — offer to create a new Brain page:

- **Analysis or comparison** → `wiki/analysis/YYYY-MM-DD-slug.md`
- **Project-specific insight** → update the relevant `pm/projects/` page
- **New concept or entity discovered** → `wiki/concepts/` or `wiki/entities/`
- **Corrects or updates existing knowledge** → update the existing page directly

This is how questions compound into permanent knowledge. The user decides whether to file.

If filed:
- Create the page with proper frontmatter, wikilinks, and claim-level source links
- Update the relevant index
- Update overview if the filing shifts the big picture
- Append to `log.md`:

```
## [YYYY-MM-DD] query | Question summary
Answer filed as [[path/to/new-page]]. Sources consulted: [[page1]], [[page2]]. Connectors queried: [list].
```

If not filed, still log the query if it was substantive:

```
## [YYYY-MM-DD] query | Question summary
Sources consulted: [[page1]], [[page2]]. Answer provided to chat (not filed).
```
