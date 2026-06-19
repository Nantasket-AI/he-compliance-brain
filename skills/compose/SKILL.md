---
name: compose
description: "Compose a message (email, Teams message, Slack post, etc.) grounded in Brain knowledge. Pulls project state, meeting decisions, entity context, and live connector data. Always presents a draft for approval before sending."
argument-hint: "<format> <topic or recipient> — e.g. 'email to Jane about API migration progress' or 'teams message to Alex re: sprint timeline'"
---

# /the-brain:compose — Draft a Message from Brain Context

Compose a professional message in the requested format (email, Teams message, Slack post, meeting invite body, etc.) that is grounded in the Brain's accumulated knowledge and live connector data. The message should sound like *you* wrote it — informed, specific, and contextually aware.

**CRITICAL**: This skill NEVER sends, posts, or delivers anything. It ALWAYS presents a draft for the user to review, edit, and approve. Only after explicit user confirmation ("send it", "post it", "looks good, go ahead") should the message be delivered — and only if a connector supports it.

## Step 1: Parse the request

Determine from the user's input:
- **Format**: email, Teams message, Teams channel post, Slack message, meeting invite, Confluence comment, Jira comment, generic text, etc.
- **Recipient(s)**: names or roles — resolve to entity pages in `wiki/entities/` for context
- **Topic**: what the message is about — map to project(s) in `pm/projects/`, meeting(s) in `pm/meetings/`, or concepts in `wiki/`
- **Tone**: infer from context (status update → professional/concise, follow-up → friendly/action-oriented, escalation → direct/clear, stakeholder comms → polished)
- **Urgency/timing**: is this time-sensitive? Does it reference a deadline?

If the request is ambiguous, ask the user to clarify before proceeding.

## Step 2: Gather Brain context

Navigate the Brain top-down (per CLAUDE.md navigation sequence) to collect relevant facts:

1. **Project context**: Read the relevant project page(s) in `pm/projects/` — current status, recent decisions (from decision log), open questions, next milestones, stakeholders
2. **Meeting context**: If the message references a meeting or follows up on one, read the meeting page in `pm/meetings/` — decisions, action items (with owners and due dates), key discussion points
3. **Entity context**: Read entity pages for all recipients and mentioned people — their role, relationship to the project, what they care about, recent interactions
4. **Task context**: Check `planner/tasks.md` for relevant open/completed tasks
5. **Recent activity**: Check today's daily file and `log.md` for recent work on the topic

**Key**: Collect specific facts, decisions, dates, and action items — the message should contain *concrete* information, not vague summaries.

## Step 3: Gather live state from connectors (if needed)

If the message needs current data beyond what the Brain has:

- **Jira**: current ticket status, recent updates, sprint state — for status updates or ticket-related messages
- **Outlook calendar**: upcoming meeting times, attendee lists — for scheduling messages or meeting follow-ups
- **Outlook email**: recent email thread context — to maintain conversational continuity (check if there's an existing thread to reply to)
- **Teams**: recent messages in relevant chats — to understand the conversation context if replying to a thread
- **SharePoint**: document links or recent edits — if the message needs to reference shared documents

## Step 4: Draft the message

Compose the message with:

- **Subject line** (for email/formal formats): clear, specific, action-oriented
- **Greeting** appropriate to the format and relationship (email gets "Hi [Name],", Teams message might be more casual)
- **Body**: organized logically — context → update/request → next steps. Ground every claim in Brain knowledge. Include:
  - Specific dates, decisions, and action items (not vague references)
  - Links to relevant resources (Jira tickets, SharePoint docs, Confluence pages) where appropriate
  - Clear asks or next steps if this is an action-oriented message
- **Closing** appropriate to format
- **Tone**: match the inferred or requested tone. Default to professional but approachable.

**Formatting rules by format**:
- **Email**: full professional structure (subject, greeting, paragraphs, sign-off). Can be longer.
- **Teams message**: concise, can use bullet points. Skip formal greeting if the chat context is casual.
- **Teams channel post**: slightly more structured than DM. May include headers or bullets for scan-ability.
- **Jira/Confluence comment**: technical, direct, reference-heavy. Use markdown formatting.
- **Meeting invite body**: agenda-style. Include: purpose, prep needed, relevant links.
- **Generic**: plain text, user decides where to paste it.

## Step 5: Present the draft for approval

Display the draft clearly, prefixed with metadata:

```
**Format**: [email / Teams message / etc.]
**To**: [recipient(s)]
**Subject**: [if applicable]
**Context**: [1-line summary of what Brain knowledge informed this]

---

[DRAFT MESSAGE]

---
```

Then ask: **"Ready to send, or want changes?"**

**Available actions after approval**:
- **Email**: If user approves, inform them the draft is ready to paste into Outlook (or if the email connector supports compose, offer to send — but ONLY after approval)
- **Teams message**: Inform user the draft is ready to paste into Teams
- **Jira comment**: Can post via Jira connector (`addCommentToJiraIssue`) — but ONLY after explicit approval
- **Confluence comment**: Can post via Confluence connector — but ONLY after explicit approval
- **Other formats**: Present as copyable text

## Step 6: Log (if substantive)

If the message was substantive (project update, stakeholder comms, decision notification), append to `log.md`:

```
## [YYYY-MM-DD] system | /the-brain:compose — [format] to [recipient] re: [topic]
Drafted [format] grounded in [[project-page]], [[meeting-page]]. [Sent/Not sent — user copied manually].
```

Also consider: if the message captures a decision or commitment, should the relevant project page or meeting page be updated? Offer to update if appropriate.
