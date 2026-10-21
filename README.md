# Claude Skills

Skills I've built for Claude, mostly to take the busywork out of project management. Each folder is one self-contained skill.

| Skill | What it does |
|---|---|
| [Daily Sprint Digest](daily-sprint-digest/) | Turns a day of Jira and GitHub activity into an end-of-day sprint readout ready to paste into Slack, and flags work that's stalled, slow, or waiting on a stakeholder. |

## Using a skill

1. Download the skill's folder (or the whole repo with **Code → Download ZIP**).
2. Add the folder to Claude as a skill. In Claude Code, put it in `~/.claude/skills/`; in the Claude app, zip the folder and upload it under skills settings.
3. Follow the setup steps in that skill's README.

## What's a skill?

A skill is a folder with a `SKILL.md` file of instructions, plus any reference files it needs. Claude loads it when a request matches the skill's description, so the same job gets done the same way every time.
