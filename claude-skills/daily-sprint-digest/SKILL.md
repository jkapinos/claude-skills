---
name: daily-sprint-digest
description: Build an end-of-day sprint readout from Jira and GitHub. Sorts every ticket in the active sprint into Completed, Progress Made, Stalled, and Not Started; compares today against the last five readouts; and returns a paste-ready Slack update for the team, a short leadership summary, and a private "For you" list of callouts with suggested follow-ups. Use when asked for a daily sprint update, standup summary, end-of-day readout, sprint digest, or "what moved today", and when a scheduled task runs it. Also use to revise a readout already produced in the conversation ("move PROJ-12 to stalled", "shorten the leadership version").
---

# Daily Sprint Digest

Turn the last business day of Jira and GitHub activity into three things: a team update ready to paste into Slack, a three-to-four line leadership summary, and a private list of callouts for the PM. The PM decides what to do with each callout; the skill only recommends.

## 0. Load the config

Read `config.md` in this skill folder (copy `references/config-template.md` to create it on first use). It holds the Jira project and board, GitHub repos, team roster, history location, thresholds, and waiting signals. If a value is missing, use the template default and list what was assumed under **Setup notes** at the end of the output.

## 1. Set the window

- Window end: now. Window start: the same time on the previous business day.
- On Monday (or the first business day after a holiday in `config.md`), the window starts at the previous business day's run time, so Friday evening and the weekend are included.
- On weekends and listed holidays, do nothing unless asked directly.
- State the window at the top of the private section, e.g. "Covers Fri 4:00pm – Mon 4:00pm ET".

## 2. Gather the data

Use whatever Jira and GitHub tools are connected (MCP connectors, `gh` CLI, or REST). Read only; never change tickets, comment, or post anywhere.

**Jira** (active sprint on the configured board):
- Sprint name, start and end dates, sprint goal.
- Every issue in the sprint: key, summary, type, status, assignee, story points, flagged state, labels, and the issue changelog (status transitions with timestamps).
- Comments added inside the window, plus the most recent comment on any In Progress or Blocked issue.

**GitHub** (configured repos):
- PRs opened, updated, reviewed, merged, or closed in the window, and commits pushed in the window.
- Link activity to a ticket when the ticket key appears in the branch name, PR title, PR body, or commit message. Activity with no key goes in "Unlinked work" in the private section, never dropped silently.

If a source fails, keep going with what you have and say which source was missing in **Setup notes**. Never fill gaps by guessing.

## 3. Bucket every sprint ticket

Each ticket lands in exactly one bucket, checked in this order:

1. **Completed**: moved to a done status (per `config.md`) inside the window.
2. **Stalled**: in an active status and either (a) carries a waiting signal (step 4), or (b) has had no activity for longer than its stall threshold. Activity means a status change, commit, PR event, or comment.
3. **Progress Made**: any activity in the window that isn't a completion.
4. **Not Started**: still in a to-do status with no activity ever.

In-progress tickets with no activity today but still inside their stall threshold go under Progress Made as "no change today", so nothing goes missing.

**Stall thresholds scale with story points** (business days without activity; override in `config.md`):

| Points | Stalled after |
|---|---|
| 1–2 | 1 day |
| 3 | 2 days |
| 5 | 3 days |
| 8+ | 4 days |
| Unpointed | 2 days |

## 4. Detect "waiting on a stakeholder"

A ticket is waiting when any of these is true:
- Its status is Blocked (or a status listed as blocked in `config.md`), or it is flagged.
- It carries a waiting label from `config.md` (default `waiting-on-stakeholder`).
- Its most recent comment matches a waiting phrase from `config.md` (defaults: "waiting on", "waiting for", "pending", "need from", "needs input", "following up", "blocked by", "on hold") and nothing has happened since.

When the comment names the person or team being waited on, carry that name into the callout.

## 5. Compare against history

Two sources, used together:

- **Jira changelog** is the source of truth for how long a ticket has been in its current status. It works even on the first run.
- **Saved readouts**: load the last five from the history location in `config.md`. Use them to spot repeats and trends, such as a ticket that has been in Stalled three readouts running, or one that was flagged yesterday and is still flagged.

Raise a callout for any of these:
- **Hasn't moved**: same bucket and no activity across two or more of the last five readouts.
- **Slower than expected**: in progress longer than the expected cycle time for its points (1–2 pts: 2 days; 3 pts: 3 days; 5 pts: 5 days; 8+ pts: 7 days; overridable).
- **Waiting on a stakeholder**: from step 4, with how long it has been waiting.
- **Sprint pace**: the share of sprint points completed trails the share of sprint days elapsed by more than 15 points (e.g. 60% of the sprint gone, 40% of points done).
- **Late starters**: Not Started tickets once more than half the sprint has passed.
- **Reopened or bounced**: moved back from a review, QA, or done status.
- **Scope change**: tickets added to or removed from the sprint inside the window.

Rank callouts by risk to the sprint goal, highest first. Keep it to the ones worth acting on; if nothing qualifies, say "Nothing to chase today."

## 6. Write the output

Use the exact layout in `references/output-format.md`. Three parts, in this order:

1. **Team update**: paste-ready for Slack.
2. **Leadership summary**: three or four lines, paste-ready.
3. **For you (private)**: callouts, each with a suggested follow-up and a one-line draft message, then unlinked work and setup notes.

Writing rules:
- One line per ticket: key, a plain-language description of what happened, and the person. "PROJ-142 Checkout address validation: PR merged, moved to QA (Dana)". Describe what changed, not just the status name.
- Tight but specific. No filler such as "great progress today" or "the team continued working on".
- Use Slack-safe formatting only: bold section labels, bullets, links, and an emoji per section header if `config.md` turns them on. Slack has no underline, headings, or tables; never use them in the paste-ready parts.
- Use `@name` for people only if `config.md` maps names to Slack handles; otherwise plain first names.
- Quiet days still get a readout: "No movement on sprint work today" plus the Stalled list.

## 7. Save the readout

After producing the output, save it as `YYYY-MM-DD.md` in the history location (a `readouts/` folder in a GitHub repo by default, since scheduled runs start fresh and local files don't survive). Include a small machine-readable block at the bottom listing each ticket key with its bucket and status, so future runs can compare without re-parsing prose. Keep the most recent 30; never delete anything else.

If saving fails, say so in Setup notes and still return the readout.

## 8. Revisions

The PM edits by talking to Claude: "move PROJ-12 to Stalled", "drop the Not Started list", "make the leadership summary about the checkout launch", "add that design sign-off landed". Apply the change, return the full updated team update and leadership summary (not just the changed line), and re-save the day's readout file so tomorrow's comparison uses the edited version. Treat a manual move as a fact for that ticket's history.
