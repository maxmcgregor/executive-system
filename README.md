# Executive System

A personal executive system powered by Claude Code. Strategic direction, accountability, and guard rails -- all through structured conversations.

## What This Does

This system runs three feedback loops at three speeds:

- **Daily** (`/start`) -- Decide what to work on today based on your goals and recent progress
- **Weekly** (`/weekly-review`) -- Compare what you did against what you committed to
- **Monthly** (`/board-meeting`) -- Full strategic review with a board of advisors

It keeps you honest about whether your daily work is moving you toward your bigger goals.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (CLI, desktop app, or IDE extension)

## Setup

1. Clone this repo
2. Open it in Claude Code
3. Say hello

That's it. Claude walks you through the rest.

## What Happens Next

Claude detects that the system is new and starts an onboarding conversation. Over 2-3 sessions, you'll define:

- **Your vision** -- the life you're building toward
- **Your values** -- the filters for every decision
- **Your profile** -- how you work, what drains you, where you tend to fail
- **Your board** -- 8 perspectives that challenge your thinking (customizable)
- **Your goals** -- 2-3 controllable targets for this quarter

Then you run your first board meeting and you're operational.

## The Habit Loop

Four commands. Everything else is optional.

| Command | When | Time |
|---|---|---|
| `/start` | Beginning of each work session | 2-3 min |
| `/log` | End of each work session | 1-2 min |
| `/weekly-review` | Fridays | 5-10 min |
| `/board-meeting` | First Friday of each month | 30-60 min |

Run `/how-to-use` for the full guide on why each piece matters.

## Other Commands

| Command | Purpose |
|---|---|
| `/journal` | On-demand reflective writing with probing questions |
| `/capture` | Quick idea capture to the backlog (no evaluation, just save) |

<details>
<summary>File structure</summary>

```
executive-system/
├── CLAUDE.md              # System brain -- how Claude operates this system
├── ONBOARDING.md          # Tracks setup progress
├── VALUES.md              # Your values and principles
├── VISION.md              # The life you're building toward
├── PROFILE.md             # Your work style, strengths, failure modes
├── config.md              # System preferences (auto-commit, etc.)
├── board/                 # 8 advisor perspectives (customizable)
├── goals/                 # Quarterly goals
├── indicators/            # Metrics you're watching
├── experiments/           # Hypotheses you're testing
├── plans/                 # Execution plans
├── backlog/               # Captured ideas (triaged monthly)
├── reviews/weekly/        # Weekly review outputs
├── reviews/board/         # Monthly board meeting outputs
├── logs/build/            # Daily build logs
├── logs/journal/          # Journal entries
├── research/              # Your reference material
├── projects/              # Active project directories
└── skills/                # Claude Code slash commands
```

</details>

## Note

This system is built specifically for Claude Code. It uses Claude Code skills (slash commands) and relies on Claude reading and writing markdown files in this repo. It does not work with other AI tools.
