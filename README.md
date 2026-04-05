# Executive System

A personal executive system powered by Claude Code. Strategic direction, accountability, and guard rails -- all through structured conversations.

## What This Does

This system runs three feedback loops at three speeds:

- **Daily** (`/start`) -- Decide what to work on today based on your goals and recent progress
- **Weekly** (`/weekly-review`) -- Compare what you did against what you committed to
- **Monthly** (`/board-meeting`) -- Full strategic review with a board of advisors

It keeps you honest about whether your daily work is moving you toward your bigger goals.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (CLI, desktop app, or IDE extension). If you don't have it yet, follow the install instructions at that link -- it takes a few minutes.

## Setup

1. **Download this repo.** Click the green **Code** button near the top right of this page. Copy the HTTPS URL. Open your terminal and run:
   ```
   git clone https://github.com/maxmcgregor/executive-system.git
   ```
   (If you don't have git installed, Claude Code can help you set it up -- just ask.)

2. **Open it in Claude Code.** In your terminal:
   ```
   cd executive-system
   claude
   ```

3. **Say hello.** Type anything -- "hello", "start", whatever. Claude takes it from there.

That's it. If you get stuck at any point, just tell Claude what's happening and it'll help you through it.

## What Happens Next

Claude detects that the system is new and starts an onboarding conversation. Over 2-3 sessions, you'll define:

- **Your vision** -- the life you're building toward
- **Your values** -- the filters for every decision
- **Your profile** -- how you work, what drains you, where you tend to fail
- **Your board** -- 8 perspectives that challenge your thinking (customizable)
- **Your goals** -- 2-3 controllable targets for this quarter

Then you run your first board meeting and you're operational.

**Tip:** During onboarding, the system will recommend free personality assessments ([Big Five](https://bigfive-test.com), [Enneagram](https://www.truity.com/test/enneagram-personality-test)). These are optional but make a real difference -- the better your profile, the better the system calibrates feedback, reviews, and pattern detection to how you're actually wired.

## The Habit Loop

Five commands. `/capture` is the only optional one.

| Command | When | Time |
|---|---|---|
| `/start` | Beginning of each work session | 2-3 min |
| `/log` | End of each work session | 1-2 min |
| `/journal` | 1-2x per week (when something's brewing) | 5-15 min |
| `/weekly-review` | Fridays | 5-10 min |
| `/board-meeting` | First Friday of each month | 30-60 min |

`/capture` saves ideas to the backlog anytime. Run `/how-to-use` for the full guide on why each piece matters.

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
