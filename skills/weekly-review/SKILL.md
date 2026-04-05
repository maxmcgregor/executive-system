---
name: weekly-review
description: Weekly accountability check - compares what you did vs what you committed to (Fridays)
---

# /weekly-review

A Friday ritual. Generates an honest assessment of the week, then gives the user space to add context.

## How It Works

1. **Read the data** (silently, before responding):
   - `logs/build/` -- all build logs since the previous weekly review date (inclusive of that date, to capture any work logged after the review ran). If no previous review exists, use last 7 days.
   - `goals/` -- current quarter's goals
   - `experiments/` -- active experiments
   - `plans/` -- active plans (check checkbox progress against the week's build logs)
   - `VALUES.md` -- for filtering assessment
   - `PROFILE.md` -- known failure modes to watch for
   - `reviews/weekly/` -- previous weekly review (for continuity)

2. **Generate the assessment:**

   Claude drafts the entire review from build logs and goal status.

   Structure:
   ```
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
   ```

3. **Present to user and ask for input:**
   - "Here's the week. Anything to add, correct, or context I'm missing?"
   - User adds their commentary (defending decisions, adding context like travel/illness, noting things the logs didn't capture)

4. **Incorporate user's input and save the final review.**

## What to Flag

- **Behavioral drift:** "Goal calls for weekly blogging. Build logs show only coding activity this week."
- **Stalled projects:** "Project X hasn't appeared in build logs for N days."
- **Consistency gaps:** "Build logs show 3 of 7 days this week. Previous weeks averaged 5."
- **Positive momentum:** Flag when things ARE working. "Third consecutive week of consistent blogging."
- **Plan avoidance:** "Launch plan calls for daily community participation. Build logs show 0 days this week."
- **Plan progress:** "X of Y checkboxes completed in [plan name] this week. On pace / behind / stalled."
- **Shiny object (with diagnosis):** "Build logs show work on [new thing] outside current goals. Worth asking: is the current work feeling routine, or is this a genuine opportunity?" Don't just flag -- help distinguish stimulation-seeking from strategic pivot.

## Tone

- Honest, not harsh. Not a cheerleader, not a drill sergeant.
- **Present data like a dashboard, not a report card.** State facts without judgment framing. "Build logs show coding 5 days, writing 0 days" -- not "You failed at writing" or "You committed to X but didn't."
- Adapt tone to `PROFILE.md` communication preferences.
- Acknowledge context. If the user says they were traveling, that's legitimate -- note it and move on.
- The review should take 5-10 minutes total, including user input.

## Saves To

`reviews/weekly/YYYY-WXX.md`

Include both the generated assessment and user's commentary in the saved file.

## Empty-State Branches

- **No goals:** Summarize build logs only. Ask: "Want to set goals now or defer to your first board meeting?"
- **0-1 build logs:** Light weekly reflection. "What did you work on this week? What's the plan for next week?"
- **No previous review:** Skip comparison to last week. Just present this week's data.
- **No experiments:** Skip the Experiments Status section entirely.
- **No plans:** Skip the Plan Progress section entirely.

## Important

- This is primarily a report, not a conversation. Generate the assessment, take brief input, save.
- User's commentary is captured verbatim and saved alongside the assessment. This becomes data for the monthly board meeting.
- If the user consistently makes excuses for the same issue across multiple weeks, the board meeting will surface that pattern. The weekly review just captures it.
