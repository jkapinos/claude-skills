# Daily Sprint Digest config

Copy this file to `config.md` in the skill folder and fill it in. Anything left blank uses the default shown.

## Jira
- site: your-team.atlassian.net
- project_key: PROJ
- board: (board name or ID; the active sprint is used)
- done_statuses: Done, Closed, Released
- todo_statuses: To Do, Backlog, Selected for Development
- blocked_statuses: Blocked, On Hold

## GitHub
- repos: your-org/web-app, your-org/api
- match ticket keys in: branch, PR title, PR body, commit message

## Team
Map names to Slack handles to get @-mentions; leave blank for plain first names.
- Dana Lee: @dana
- Priya Shah: @priya

## Schedule
- timezone: America/New_York
- run_time: 16:00
- business_days: Mon–Fri
- holidays: (dates, one per line, YYYY-MM-DD)

## History
- location: github:your-org/sprint-digests/readouts
- keep: 30

## Stall thresholds (business days without activity)
- 1–2 pts: 1
- 3 pts: 2
- 5 pts: 3
- 8+ pts: 4
- unpointed: 2

## Expected cycle time (business days in progress)
- 1–2 pts: 2
- 3 pts: 3
- 5 pts: 5
- 8+ pts: 7

## Waiting signals
- labels: waiting-on-stakeholder
- phrases: waiting on, waiting for, pending, need from, needs input, following up, blocked by, on hold

## Output
- emoji: on
- slack_markup: rendered   (or: mrkdwn)
- sprint_pace_gap: 15      (percentage points)
