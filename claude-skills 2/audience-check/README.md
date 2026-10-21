# Audience Check

A Claude skill that reviews a message through the eyes of the specific person or team who will read it, before you hit send.

You keep a short profile for each audience you write to often: how they read, the terms they use differently, what causes friction, and, most usefully, past moments where communication broke down. When you draft something for them, the skill flags what's likely to confuse or frustrate them, explains why using that profile, and hands back a revised draft.

## Why

Most miscommunication between technical and business teams isn't about effort. It's about words that mean different things to different people. "The fix is done" means merged to an engineer and live to Finance. A profile turns those lessons into something you check every time, instead of relearning them.

## Example

Draft to the fictional Finance Lead in `profiles/example-finance-lead.md`:

> Hey Riley! Quick ask, the duplicate order fix is done so you should be good to close. There was also a minor data issue with the order sync yesterday, we're looking into it.

What the skill returns, in short:

**Verdict:** Rework before sending. "Done" has caused a bad close before, and the data issue has no size.

**Flags**
1. **"the duplicate order fix is done"** (Confusing): Riley reads "done" as corrected in the ledger, which led to two days of rework last time. *Try:* "The duplicate order fix was deployed Tuesday at 3pm ET, and October data is corrected."
2. **"minor data issue"** (Missing): no size given, and a past "minor" issue went unnoticed for a week. *Try:* "About 40 orders (~$3K) from Monday didn't import. [CONFIRM COUNT]"
3. **"order sync"** (Confusing): not Riley's term. *Try:* "the nightly order import into the ledger."
4. **"Hey Riley! Quick ask"** (Tone): it's close week, and the message has no actual ask.

**Revised draft**
> Riley, two updates before you close October:
> - **Duplicate orders:** fix deployed Tue 3pm ET; October data is corrected. Nothing needed from you.
> - **Missing orders:** about 40 orders (~$3K) from Monday didn't make it into the nightly import to the ledger. We'll have them added by Thu 12pm ET.
>
> **Ask:** hold October close until Thursday noon, or tell me if that doesn't work.

**Open questions:** confirm the missing order count and dollar amount.

## Two modes

- **Check a draft:** "Check this before it goes to Riley." Returns a verdict, up to 7 flags (Confusing, Friction, Missing, Tone), a revised draft, and open questions.
- **Build or update a profile:** paste writing samples, a thread where things went sideways, or your own notes. The skill fills in `references/profile-template.md` and asks you to correct it before use. When a message lands badly, tell it what happened and it adds the lesson to that profile.

## Setup

1. Add the `audience-check` folder to Claude as a skill.
2. Build your first profile: "Build an audience profile for [name/team]," then paste samples and context.
3. Use it on your next draft: "Check this for [name/team]."

Keep profiles professional: they describe how someone prefers to communicate, not judgments about them, and shouldn't include sensitive personal details.

## Files

```
audience-check/
├── SKILL.md
├── README.md
├── references/
│   └── profile-template.md
└── profiles/
    └── example-finance-lead.md   # fictional example
```

Inspired by an audience-profile exercise from a Claude training, and by years of translating between engineering and business teams.
