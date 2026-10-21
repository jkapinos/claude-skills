# Output format

Render as normal markdown in the chat (not in a code block). Copying rendered markdown from Claude into Slack keeps bold, italics, bullets, and links. Slack has no underline, headings, or tables, so the paste-ready parts use bold labels instead.

Use a horizontal rule between the three parts so they are easy to select separately.

---

**Team update to paste**

**Sprint 14 · Day 6 of 10 · Wed Oct 21**
_Goal: ship guest checkout to 10% of traffic_

✅ **Completed (2)**
- KEY-123 Short description of what finished (Name)

🔄 **Progress Made (4)**
- KEY-130 What changed today, e.g. PR opened for review (Name)
- KEY-131 No change today, still in development (Name)

⚠️ **Stalled (2)**
- KEY-140 Waiting on Legal for copy approval, 3 days (Name)
- KEY-141 No activity for 2 days, 1 pt (Name)

⏳ **Not Started (3):** KEY-150, KEY-151, KEY-152

**Sprint pace:** 18 of 34 points done (53%) at 50% of the sprint.

---

**Leadership summary to paste**

**Sprint 14 · Day 6/10:** On track for guest checkout; 53% of points done at the halfway mark. One risk: checkout copy is waiting on Legal (3 days), which gates the 10% rollout. No scope changes today.

---

**For you (private, don't paste)**
_Covers Tue 4:00pm – Wed 4:00pm ET · compared with the last 5 readouts_

1. **KEY-140 is waiting on Legal (3 days, flagged in 3 of the last 5 readouts).** Gates the sprint goal.
   Suggested: DM Legal's contact, then add a line to the group update if there's no answer by tomorrow.
   Draft: "Hi Sam, checking on the checkout copy approval for KEY-140. It's the last gate before our 10% rollout. Any chance we can have it by Thursday?"
2. **KEY-141 hasn't moved in 2 days (1 pt).**
   Suggested: quick DM to the assignee.
   Draft: "Hey Priya, anything blocking KEY-141? Happy to help clear it."

**Unlinked work:** PR #88 "fix flaky test" (no ticket key)
**Setup notes:** none

---

## Rules for each part

- **Counts** in bucket headers always match the number of tickets listed.
- **Not Started** is a single line of keys. Expand to one line per ticket only when more than half the sprint has passed.
- **Emoji** in headers only if `config.md` has `emoji: on` (default on). With it off, use bold labels alone.
- **Leadership summary**: no ticket-by-ticket detail; sprint progress, the top risk or two, and anything leadership needs to decide. Plain language, no ticket keys unless one is the risk.
- **For you** callouts: numbered, highest risk first; each has the issue in bold, a "Suggested:" line choosing between a direct message and the group update (or both, in order), and a "Draft:" line written in a friendly, direct tone. Never paste-ready to a channel.
- **Slack API mode** (only if `config.md` has `slack_markup: mrkdwn`): use `*bold*`, `_italic_`, `<url|text>` links, and `•` bullets, inside a code block so it can be copied raw.
