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

1. **Download this repo.** Open your terminal and run:
   ```
   git clone https://github.com/maxmcgregor/executive-system.git
   ```

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
- **Your current work** -- everything in flight, with the next action on each
- **Your goals** -- 2-3 controllable targets for this quarter

Then you run your first board meeting and you're operational.

Don't skip the current-work step. It's the one that decides whether `/start` is useful tomorrow
morning -- a project you forgot to mention is a project the system can never surface. List the stalled
and half-finished ones too.

**Tip:** During onboarding, the system will recommend free personality assessments ([Big Five](https://bigfive-test.com), [Enneagram](https://www.truity.com/test/enneagram-personality-test)). These are optional but make a real difference -- the better your profile, the better the system calibrates feedback, reviews, and pattern detection to how you're actually wired.

## The Habit Loop

Five commands carry the whole system. Start with `/start` and `/log` -- if those two stick, everything
else has data to work with.

| Command | When | Time |
|---|---|---|
| `/start` | Beginning of each work session | 2-3 min |
| `/log` | End of each work session | 1-2 min |
| `/journal` | 1-2x per week (when something's brewing) | 5-15 min |
| `/weekly-review` | Fridays | 5-10 min |
| `/board-meeting` | First Friday of each month | 30-60 min |

**Pull these when you want them.** None are scheduled:

| Command | What it's for |
|---|---|
| `/capture` | An idea arrives. Save it, move on, let the board judge it next month. |
| `/lens` | You want a straight read. Pick a vantage point -- skeptic, future self, business, or one you name -- and it reads your files *before* it speaks, then opens with what it found: patterns, with dates. |
| `/dump-review` | You're at a "what do I do next?" fork. It reads everything you've saved and journaled, names the threads that keep recurring across months, and checks them against what your build logs say you actually did. |

Run `/how-to-use` for the full guide on why each piece matters.

## Tracking More Than One Thing

Once you have two or more efforts running, `state/projects.md` tells you *how each one is doing* but
not *what step comes next inside it*. That's what `INITIATIVES.md` is for.

Each effort becomes an **initiative** with an ID like `blog-seo`, and each step inside it a numbered
**story** like `blog-seo.2`. The same ID goes in the registry, the plan, and the build log when the
step ships -- so `grep blog-seo` months later reconstructs the whole effort, and "what's next on this?"
has one deterministic answer instead of being a judgment call every morning.

It ships with a worked example to replace, and it's genuinely optional -- with one project running, skip
it.

## How It Stays Fast and Honest

The system keeps two kinds of record, and never mixes them:

- **The history** -- your daily build logs (`logs/build/`) and git. Append-only. Nothing is ever lost.
- **The current snapshot** -- three small files in `state/` that hold only what's true *right now*:
  your goals and their status, what each project is up to, and your live strategic direction.

`/start` reads the snapshot first, so it knows where things stand in seconds without re-reading
weeks of logs. `/log` updates the snapshot at the end of each session by **overwriting** it with the
current truth -- finished items drop out (the history still has them), open items carry forward. That
overwrite rule is what keeps the snapshot small and trustworthy instead of growing into a pile of
stale notes. You don't manage any of this; the skills do it for you.

<details>
<summary>File structure</summary>

```
executive-system/
├── CLAUDE.md              # System brain -- how Claude operates this system
├── ONBOARDING.md          # Tracks setup progress
├── INITIATIVES.md         # Optional: what's next inside each effort you have running
├── VALUES.md              # Your values and principles
├── VISION.md              # The life you're building toward
├── PROFILE.md             # Your work style, strengths, failure modes
├── config.md              # System preferences (auto-commit, etc.)
├── context-map.yaml       # Domain->resource routing for scoped context loading
├── state/                 # Current-truth snapshot read at the start of every session
├── board/                 # 8 advisor perspectives (customizable)
├── goals/                 # Quarterly goals
├── indicators/            # Metrics you're watching
├── experiments/           # Hypotheses you're testing
├── plans/                 # Execution plans
├── backlog/               # Captured ideas (triaged monthly)
├── reviews/weekly/        # Weekly review outputs
├── reviews/board/         # Monthly board meeting outputs
├── reviews/dump/          # Dump-review outputs (periodic cross-corpus synthesis)
├── logs/build/            # Daily build logs (the append-only history)
├── logs/journal/          # Journal entries
├── research/              # Your reference material
├── archive/               # Finished/abandoned docs, out of the hot path
├── projects/              # Active project directories
└── skills/                # Claude Code slash commands
```

</details>

## Note

This system is built specifically for Claude Code. It uses Claude Code skills (slash commands) and relies on Claude reading and writing markdown files in this repo. It does not work with other AI tools.
