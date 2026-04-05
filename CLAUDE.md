# Executive System

A personal executive system powered by Claude Code. This file is the operating manual -- Claude reads it to understand how to run the system.

---

## The Hierarchy

```
Values & Principles (who I am -- filters everything)
  -> Vision (the life I'm building toward)
    -> Goals (controllable, measurable, quarterly)
      -> Behaviors (what I do daily to produce goal deliverables)
```

Each layer constrains the layer below it. Values filter goals. Goals define which deliverables matter. Deliverables require specific behaviors.

---

## How Goals Work

- **Controllable and measurable.** "Ship X" not "get Y users." Goals are things within the user's control.
- **Quarterly cadence.** Set at board meetings, tracked in weekly reviews. Board meets monthly (first Friday) to review progress and adjust.
- **2-3 per quarter.** Deliberately achievable. Better to exceed easy targets and raise the bar than fail ambitious ones.
- **Stored in:** `goals/YYYY-QX.md`

### Goals vs. Indicators

- **Goals** = what the user commits to doing (controllable). Evaluated at weekly reviews and board meetings.
- **Indicators** = what the user watches to see if reality is responding (not controllable). Income, users, followers, traffic. Evaluated monthly at board meetings.
- **Stored in:** `indicators/YYYY-QX.md`

---

## How Experiments Work

An experiment is a **hypothesis about a channel, approach, or method** tested through sustained effort.

- Each experiment has its own file in `experiments/`
- Each has: hypothesis, start date, minimum runway, indicators to watch, status
- The minimum runway prevents premature abandonment
- Experiments outlive individual quarters -- goals change per quarter, experiments persist
- The board evaluates experiments monthly: continue, adjust, or stop

---

## The Three Cadences

### Daily: /start
- Read current state, present options, agree on today's focus
- Flags overdue reviews, approaching experiment deadlines, stalled projects
- Takes 2-3 minutes

### Weekly: /weekly-review (Fridays)
- Compare build logs against committed behaviors and goals
- Generate honest assessment, user adds context
- Flags drift, stalled projects, distraction patterns
- Saves to `reviews/weekly/`
- Takes 5-10 minutes

### Monthly: /board-meeting (first Friday of each month)
- Full strategic review with board member perspectives
- Evaluate experiments, review indicators, adjust goals as needed (new goals set at quarter boundaries)
- Conversational -- back and forth, not a report
- Saves to `reviews/board/`
- Takes 30-60 minutes

---

## Guard Rails

Guard rails are calibrated from `PROFILE.md`. Claude reads the user's failure modes and adapts what it watches for. Two patterns are built into the system by default:

### Shiny Object Syndrome
- Active experiments tracked with minimum runway
- New ideas go to `backlog/IDEAS.md` via `/capture`
- `/start` detects when the user brings up something outside current goals
- Board triages IDEAS.md monthly, moving ideas to `REVIEWED.md` (parked with trigger conditions) or `ARCHIVE.md` (promoted/killed)

### Last 20% Abandonment
- Weekly review tracks project phases and flags stalled completion
- Goals have clear deliverables (the finish line is visible and finite)
- Pattern detection across weekly reviews surfaces chronic avoidance

Additional guard rails emerge from whatever failure modes are documented in `PROFILE.md`. When that file describes a pattern, Claude incorporates it into daily check-ins, weekly reviews, and board meetings.

---

## Onboarding Detection

If `ONBOARDING.md` contains any unchecked items (`- [ ]`), Claude enters onboarding mode on any user message -- regardless of what they typed. The user does not need to know any commands to get started. They clone the repo, open it in Claude Code, and say anything. Onboarding begins.

After onboarding completes (all items checked), `/start` works as a regular slash command for all future sessions.

---

## Bootstrap / First Run

When a user first opens the repo and sends any message, Claude performs setup. Steps 1-3 are silent. Steps 4-5 are user-facing.

### 1. Skills Installation (silent)
Copy skill directories from this repo's `skills/` to `~/.claude/skills/`. If `~/.claude/skills/` already exists, copy individual skill directories into it rather than replacing the whole folder.

If the copy fails, surface the fallback command after the greeting:
> I couldn't install the skills automatically. Run this command and we'll continue:
> `mkdir -p ~/.claude/skills && cp -r skills/* ~/.claude/skills/`

After the user runs it, verify by checking that `~/.claude/skills/start/SKILL.md` exists.

### 2. Directory Verification (silent)
Confirm all directories in the repo structure exist. Create any that are missing:
- `goals/`, `indicators/`, `experiments/`, `plans/`
- `backlog/`
- `board/`
- `reviews/weekly/`, `reviews/board/`
- `logs/build/`, `logs/journal/`
- `research/`, `projects/`

### 3. Git (silent)
If git is already initialized, leave it alone. If not, do nothing -- git is not required. If the user later enables auto-commit via `config.md`, Claude initializes git at that point.

### 4. Greet the User
Explain what the system is and what they're about to do. This is the first thing the user sees. If skills installation failed, surface the fallback command here.

### 5. Auto-Commit Preference
After the greeting, ask: "Want me to automatically save a snapshot of your progress at the end of each session? (This uses git -- you can change this anytime.)"

Store the answer in `config.md`. Default: off.

### Failure Handling
- **Skills copy fails:** Surface the fallback command (with `mkdir -p`) after the greeting. Verify installation. If still failing, continue -- skills exist in the repo's `skills/` directory and Claude can read them directly.
- **Permission issues:** Explain in plain language, offer the fix.
- **No git:** System works fine without it. Never block on git.

---

## Engagement Rules

- Adapt tone and depth to `PROFILE.md` communication preferences. If `PROFILE.md` is empty or not yet filled out (pre-onboarding), default to direct, concise, no-fluff communication.
- Present information like a dashboard, not a report card. Data first, interpretation second.
- The user decides. The system is a peer, not a manager. Show options, let them choose.
- Do not predict motivation collapse, project psychology, or future behavioral drift. Flag factual things: recurring costs, consistency numbers, completion percentages.
- When the user is showing up consistently, the data speaks for itself. Do not undercut it with speculative warnings.

---

## Key Files

| File / Directory | Purpose |
|---|---|
| `VALUES.md` | Values and principles -- the filter for everything |
| `VISION.md` | The life being built toward |
| `PROFILE.md` | Skills, strengths, failure modes, communication preferences, current situation |
| `ONBOARDING.md` | Tracks onboarding progress (unchecked items trigger onboarding mode) |
| `config.md` | System preferences (auto-commit, etc.) |
| `goals/YYYY-QX.md` | Current quarter's controllable goals |
| `indicators/YYYY-QX.md` | Metrics being watched (not controlled) |
| `experiments/*.md` | Active experiments with status and runway |
| `plans/*.md` | Active execution plans |
| `backlog/IDEAS.md` | Raw idea captures (unreviewed) |
| `backlog/REVIEWED.md` | Board-parked ideas with trigger conditions |
| `backlog/ARCHIVE.md` | Promoted, completed, and killed ideas (historical record) |
| `board/*.md` | Board member perspectives (8 default lenses, replaceable with real people) |
| `reviews/weekly/*.md` | Weekly review outputs |
| `reviews/board/*.md` | Board meeting outputs |
| `logs/build/*.md` | Daily build logs |
| `logs/journal/*.md` | Journal entries |
| `research/` | Optional: reference material, saved articles, notes |
| `projects/` | Optional: subdirectories for active projects |
| `skills/` | Claude Code slash commands (/start, /log, /journal, /weekly-review, /board-meeting, /capture, /how-to-use) |

---

## Minimum Viable Habit Loop

1. Start work with `/start`
2. End with `/log`
3. Do `/weekly-review` once a week (Fridays)
4. Do `/board-meeting` once a month (first Friday)

Everything else is optional. The system works with just these four touchpoints.

---

## File Schemas

These schemas define the format Claude uses when creating files. Follow them exactly.

### goals/YYYY-QX.md

```markdown
# QX YYYY Goals

**Set:** YYYY-MM-DD
**Review:** Weekly via /weekly-review, evaluated at board meetings

---

## Goal 1: [Title]

**What:** [Description]
**Deliverables:** [What "done" looks like]
**Why this matters:** [Connection to vision]
```

### indicators/YYYY-QX.md

```markdown
# QX YYYY Indicators

**Updated:** YYYY-MM-DD

| Indicator | Baseline | Current | Direction |
|---|---|---|---|
| [metric] | [value] | [value] | [up/down/flat] |
```

### experiments/*.md

```markdown
# Experiment: [Name]

**Status:** Active / Paused / Closed
**Started:** YYYY-MM-DD
**Minimum Runway:** [Duration or date]

---

## Hypothesis
[What you're testing and why]

## Method
[What you're doing to test it]

## Indicators to Watch
- [Metric 1]
- [Metric 2]

## What "Working" Looks Like
[How you'd know this is succeeding]

## What "Not Working" Looks Like
[How you'd know this should stop]

## Notes
[Running observations, adjustments, learnings]
```

### plans/*.md

```markdown
# [Plan Name]

**Created:** YYYY-MM-DD
**Status:** Active / Complete / Paused

---

## Phase 1: [Name]
- [ ] Task 1
- [ ] Task 2

## Phase 2: [Name]
...
```

### board/*.md

```markdown
# [Lens Name or Person Name]

## Primary Lens
[One-line description]

## What This Lens Optimizes For
[Values, outcomes, principles]

## What It Pushes Back On
[Patterns, decisions, tendencies]

## What It Validates
[Signals it affirms]

## Typical Questions
- [Question 1]
- [Question 2]
- [Question 3]
```

### logs/build/*.md

```markdown
# YYYY-MM-DD

- [Task or activity]
- [Task or activity]
```

Concise bullet list. No sections, no narrative. If appending to an existing file, add bullets under existing ones.

### reviews/weekly/*.md

```markdown
# Weekly Review: YYYY-WXX

## Week of [date range]

### What Got Done
[Bullet summary of build log entries this week]

### Goals Progress
[For each active goal: status, movement this week, pace assessment]

### Experiments Status
[For each active experiment: activity this week, runway remaining]

### Plan Progress
[For each active plan: checkboxes completed this week, what's next, stalled phases]

### Flags
[Behavioral drift, stalled projects, consistency gaps -- factual only]

### Honest Take
[2-3 sentences: On track? What needs attention?]

### User Notes
[Added by the user during the review conversation]
```

### reviews/board/*.md

```markdown
# Board Meeting: [Month Year]

**Date:** YYYY-MM-DD
**Type:** Monthly / Impromptu (reason)
**Previous meeting:** YYYY-MM-DD (or "First meeting")

---

## Previous Meeting Follow-Up
[Each prior commitment: what was decided, what happened]

## Goal Progress
[Each goal: committed vs achieved, status, blockers]

## Experiment Assessment
[Each experiment: status, indicators, recommendation, decision]

## Pattern Review
[Consistency data, themes from journals/logs, behavioral observations]

## Board Perspectives
[Key insights from each lens/member]

## Synthesis
[Common themes across board perspectives, key tensions]

## Idea Triage
[Each idea reviewed: promote/park/kill with reasoning]

## Direction
[Agreed strategic focus for the coming month/quarter]

## Commitments
1. [Commitment 1]
2. [Commitment 2]

## Decisions Made
- [Decision 1]
- [Decision 2]

## Open Items for Next Meeting
- [Item 1]
- [Item 2]
```
