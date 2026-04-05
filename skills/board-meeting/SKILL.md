---
name: board-meeting
description: Monthly strategic review with the board - evaluates progress, sets direction, adjusts goals
---

# /board-meeting - Monthly Strategic Review

The most important ritual. Happens on the first Friday of every month, or on-demand for major strategic decisions. This is conversational -- a back-and-forth with the user, not a report.

## Meeting Framework

Every monthly board meeting follows the same 8-phase structure. This consistency ensures nothing gets skipped and creates a comparable record across months.

---

### Phase 1: Previous Meeting Review

Read the most recent file in `reviews/board/`. Compare commitments made vs. what actually happened, using evidence from build logs (`logs/build/`) and weekly reviews (`reviews/weekly/`) since that meeting.

For each commitment or decision from the previous meeting:
- **What was decided?**
- **What actually happened?**
- **Any open items that weren't resolved?**

This is accountability. Not punitive -- just honest comparison. If decisions were made and not followed through, name it. If they were followed through and the results were different than expected, name that too.

Pause for user reaction.

---

### Phase 2: Goal Progress

Read current `goals/YYYY-QX.md`. For each active goal:
- **Committed vs. achieved** (with specific evidence from build logs and weekly reviews)
- **On track, behind, or ahead?**
- **What's blocking progress, if anything?**

Present as data. Facts and numbers, not assessments of character.

At quarter boundaries: evaluate whether goals should roll over, be adjusted, or be replaced.

Pause for user input.

---

### Phase 3: Experiment Evaluation

Read `experiments/*.md` for active experiments. For each:
- **Status:** Active, approaching evaluation, past minimum runway
- **Runway consumed:** How much time/budget has been spent vs. the minimum runway
- **Indicator data:** What the numbers show (or note if data isn't available yet)
- **Recommendation:** Continue, adjust, or stop -- with reasoning

Present recommendations. User decides.

Pause.

---

### Phase 4: Pattern Review

Read all build logs (`logs/build/`) and journal entries (`logs/journal/`) since the last board meeting. Also pull behavioral flags from weekly reviews (`reviews/weekly/`).

Surface:
- **Consistency data:** Days logged, gaps, streaks
- **Repeated themes** across journal entries (what keeps coming up?)
- **Energy patterns:** What correlates with productive periods vs. stalled periods?
- **Behavioral flags** from weekly reviews (drift, avoidance, distraction patterns)
- **Wins to acknowledge** -- progress that may have been overlooked in the day-to-day

Present these as observations, not judgments. Let the user react and add context.

Pause for discussion.

---

### Phase 5: Board Perspectives

Read all `board/*.md` files. For each board lens or member:
- Apply their specific lens to the current situation
- Use their "Typical Questions" and "What It Pushes Back On" sections to shape the perspective
- Generate 2-4 sentences from that lens's point of view

Present each perspective concisely. Then synthesize: "Across the board, the common themes are..."

**Delivery calibration:** Board member files contain NO user-specific calibration. No "Engaging [User]" sections. Instead, read `PROFILE.md` at runtime and adapt delivery accordingly:
- If `PROFILE.md` describes communication preferences, follow them
- If it lists failure modes, board perspectives should address those patterns
- If `PROFILE.md` is thin or empty, default to direct, concise delivery

Pause for user reaction.

---

### Phase 6: Idea Triage

Two sources to review:

**1. New captures from `backlog/IDEAS.md`:** For each new idea, the board recommends one of:
- **Promote:** Move to active consideration (becomes an experiment, plan, or goal) -- move to `backlog/ARCHIVE.md` under Promoted
- **Park:** Move to `backlog/REVIEWED.md` with a trigger condition (what would make this relevant?)
- **Kill:** Move to `backlog/ARCHIVE.md` under Completed / Resolved / Killed

**2. Parked ideas from `backlog/REVIEWED.md`:** Re-evaluate against trigger conditions:
- Has the trigger condition been met? If so, promote or kill.
- Has context changed enough to reconsider?
- Otherwise, leave parked -- no action needed.

Criteria for evaluation:
- Does it connect to the current vision and goals?
- Does the user have relevant expertise or knowledge?
- Would the user commit sustained effort to this?
- What's the risk if pursued? What goes wrong?
- Does it have ongoing interest potential, or is it a "build once, then grind" idea? (The latter is higher risk for abandonment.)

Present recommendations. User makes final call. `backlog/IDEAS.md` should be empty after triage -- every idea gets a disposition.

Pause for user decisions.

---

### Phase 7: Direction Setting

Based on everything discussed, set the path forward:

- **Monthly commitments:** 2-3 specific, concrete, controllable things the user commits to accomplishing before the next board meeting
- **Experiment adjustments:** Any changes to active experiments
- **Strategic focus:** What gets the most energy this month? What gets deliberately deprioritized?
- **Open questions:** Anything that needs more data or thinking before deciding

At quarter boundaries, this expands to include:
- New quarterly goals (controllable, measurable, deliberately achievable -- using the goals schema from `CLAUDE.md`)
- New or adjusted indicators
- New experiments authorized from backlog

This is a conversation. The user pushes back, asks questions, adjusts. The board's recommendation is a starting point, not a mandate.

---

### Phase 8: Capture Decisions

Once the user and board align:
- Save the full board meeting to `reviews/board/YYYY-MM-DD.md`
- Update experiment files with any status changes
- Update `indicators/YYYY-QX.md` if changed
- Update backlog files based on triage decisions:
  - `backlog/IDEAS.md` -- should be empty after triage (all captures reviewed)
  - `backlog/REVIEWED.md` -- add newly parked ideas with trigger conditions, remove any promoted/killed
  - `backlog/ARCHIVE.md` -- add promoted ideas to Promoted section, add killed ideas to Completed / Resolved / Killed section
- At quarter boundaries: create or update `goals/YYYY-QX.md`
- Log any open items that should carry to the next meeting

---

## Board Meeting Output Format

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
[Common themes across board perspectives, key tensions, overall assessment]

## Idea Triage
[Each idea reviewed: promote/park/kill with reasoning]

## Direction
[Agreed strategic focus for the coming month/quarter]

## Commitments
1. [Commitment 1]
2. [Commitment 2]
3. [Commitment 3]

## Decisions Made
- [Decision 1]
- [Decision 2]

## Open Items for Next Meeting
- [Item 1]
- [Item 2]
```

---

## Empty-State Branches

- **No previous board meeting:** Skip Phase 1. Start with Phase 2 (or goal-setting if no goals exist either).
- **No goals set:** Use Phase 2 and Phase 7 to define initial goals.
- **No experiments:** Skip Phase 3. Use Phase 7 to consider starting one if appropriate.
- **No indicators:** Skip indicator review, or use Phase 7 to define initial indicators.
- **No pattern data (< 1 month of journals/logs):** Skip Phase 4. Focus on forward-looking direction.
- **No backlog items:** Skip Phase 6, or use it to brainstorm initial ideas.
- **First quarter boundary:** Full goal-setting in Phase 7. Subsequent boundaries: close out current quarter + set new goals.

---

## On-Demand Use

The user can invoke `/board-meeting` outside the monthly cadence for major strategic decisions:
- "Should I start a new project?"
- "Should I pivot this experiment?"
- "I'm thinking about a major change."

In these cases: skip the full monthly framework. Load all context, present the decision at hand, cycle through relevant board perspectives, and capture the outcome. Label these as "Impromptu" in the saved file.

---

## Tone

- This is the most serious ritual. Give it weight.
- Be honest, even when it's uncomfortable. The board's job is truth, not comfort.
- Recognize progress too -- wins matter.
- Present information, let the user think. Don't lecture.
- **Data, not evaluation.** State facts, ask questions, let the user draw conclusions.
- Adapt delivery tone from `PROFILE.md` communication preferences. If `PROFILE.md` is empty or thin, default to direct and concise.
- This should take 30-60 minutes. It's worth the time.
