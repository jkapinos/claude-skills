---
name: audience-check
description: Review a draft message, email, update, or doc against a saved profile of the person or team who will read it, and flag anything likely to confuse them, cause friction, or miss what they need, with suggested wording and a revised draft. Use whenever the user asks to check, review, or tighten something "for" a named person or team ("check this before it goes to Finance", "will Riley get this?", "draft this for the ops team"), or drafts any message to someone who has a profile in profiles/. Also use to create or update an audience profile from writing samples and past miscommunications ("build a profile for the design team", "that message to Ops landed badly, here's what happened").
---

# Audience Check

Every team reads differently. Engineering hears "done" as merged; Finance hears it as live. A message that's clear to the writer can still stall, confuse, or annoy the reader. This skill reviews a draft through one specific reader's eyes, using a profile built from how they actually write and where communication with them has broken down before.

The skill has two modes: **check a draft** and **build or update a profile**.

## Mode 1: Check a draft

### 1. Find the reader
Match the named person or team to a file in `profiles/`. If none matches, say so and offer two options: run a general check (rules in step 3 only), or build a profile first (Mode 2). Never invent traits for a reader without a profile.

### 2. Read the profile fresh
Read the whole profile every time. Pay most attention to **Past breakdowns** and **Glossary**: they are evidence of what actually went wrong, and they outrank general advice.

### 3. Review the draft
Check the draft against the profile first, then these general rules:

- **Lead with what they need.** The first two lines say what this is, what's decided, and what's needed from them, by when.
- **Name the thing.** No category words where a specific one exists ("the NetSuite sync," not "the integration"; "Thursday 5pm ET," not "end of week").
- **Translate jargon** using the profile's glossary. A term the reader has misread before is always flagged.
- **Decisions read as decisions.** Active voice, "we will," not "we could consider."
- **Blockers are labeled.** If something must happen before work can continue, it says "Blocker:" and names the owner.
- **One ask per line, with an owner and a date.** Asks buried mid-paragraph get missed.
- **Open questions in one place.** "Open question: [exact thing]," never scattered "might" and "could."
- **Never fill gaps.** If a fact, date, or decision is missing, flag it and use a placeholder like [DATE]. Don't invent specifics.

### 4. Return the review
Use this layout, and keep it tight:

**Verdict:** one line, either "Ready to send," "Send after small fixes," or "Rework before sending," plus the single biggest issue.

**Flags** (most important first, at most 7):
1. **"[quoted phrase from the draft]"**: what's wrong for this reader. *Why:* the profile evidence (a past breakdown, glossary entry, or preference). *Try:* the suggested wording.

Tag each flag with one type: Confusing, Friction, Missing, or Tone.

**Revised draft:** the full message with the fixes applied, in the same format the user will send it in (Slack, email, doc). Change only what the flags call for, and keep the user's voice.

**Open questions:** facts the user needs to fill in before sending, or "None."

If the draft is already good, say so in the verdict and keep the flags list short or empty. Don't manufacture issues.

### 5. Learn from the outcome
If the user later reports how the message landed ("they still thought it was live"), offer to add it to that profile's **Past breakdowns** using Mode 2.

## Mode 2: Build or update a profile

Inputs can be any mix of: writing samples from the reader (Slack messages, emails, docs), threads where communication broke down, and the user's own notes.

1. Copy `references/profile-template.md` to `profiles/<name>.md` (lowercase, hyphens).
2. Fill each section from the evidence. Quote short snippets rather than paraphrasing. Mark anything inferred rather than observed with "(inferred)."
3. For each breakdown, record what was said, what the reader understood, what it cost, and the rule that prevents it next time.
4. Show the user the finished profile and ask them to correct anything that's off before it's used.
5. When updating, add new evidence; don't delete old breakdowns unless the user says they no longer apply.

Keep profiles factual and professional. They describe how someone prefers to communicate, not judgments about them, and they never include sensitive personal details. Store samples only with the user's own judgment about what's appropriate to keep.

See `profiles/example-finance-lead.md` for a filled-in example (fictional).
