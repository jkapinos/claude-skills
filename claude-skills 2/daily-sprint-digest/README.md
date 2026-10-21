# Daily Sprint Digest

A Claude skill that writes an end-of-day sprint readout from Jira and GitHub, ready to paste into Slack.

Every weekday afternoon it looks at the last business day of activity in the active sprint and returns:

- **A team update** sorting every ticket into Completed, Progress Made, Stalled, and Not Started, with one plain-language line per ticket.
- **A leadership summary** in three or four lines: sprint pace, top risks, anything needing a decision.
- **A private "For you" list** of callouts worth chasing, such as tickets that haven't moved, work running slower than expected, or items waiting on a stakeholder. Each callout comes with a suggested follow-up (DM or group update) and a one-line draft message.

It compares each day with the last five readouts, so it can tell "stalled today" from "stalled all week."

## Why

Daily status updates are useful and tedious. Most of the work is collecting what changed and noticing what didn't. This skill does the collecting and noticing; the PM keeps the judgment calls, such as who to nudge and what goes in the group update.

## How it works

1. **Window:** the last business day, ending at run time. Monday covers Friday through Monday. Weekends are skipped.
2. **Data:** Jira sprint issues, changelogs, and comments; GitHub PRs and commits linked to tickets by key (e.g. `PROJ-123` in a branch, PR title, or commit message).
3. **Buckets:** stall thresholds scale with story points (a 1-point ticket stalls after a day without activity, an 8-pointer after four).
4. **Waiting on a stakeholder:** Blocked status or flag, a `waiting-on-stakeholder` label, or a latest comment like "waiting on Legal."
5. **History:** Jira's changelog gives time-in-status from day one; saved readouts add trend context.
6. **Output:** Slack-safe formatting (bold labels, bullets, links). Edits happen in conversation: "move PROJ-12 to Stalled" returns the full updated post.

It is read-only. It never changes tickets, comments, or posts to Slack on its own.

## Setup

1. Add the skill folder to Claude.
2. Connect Jira and GitHub to Claude (connectors or CLI access).
3. Copy `references/config-template.md` to `config.md` and fill in your project, board, repos, team, and history location. Readouts save to a `readouts/` folder in a GitHub repo by default, because scheduled runs start fresh and need somewhere durable to look back.
4. Schedule it: create a recurring scheduled task in Claude for weekdays at about 4pm in your time zone with the prompt "Run the daily sprint digest." Open the run to read, edit, and copy the update.

## Files

```
daily-sprint-digest/
├── SKILL.md                      # instructions Claude follows
├── README.md
└── references/
    ├── output-format.md          # exact layout of the three outputs
    └── config-template.md        # project settings and thresholds
```

## Status

v0.1, a personal project by [Jackson Kapinos](https://linkedin.com/in/jackson-kapinos). The examples use a fictional team and tickets.
