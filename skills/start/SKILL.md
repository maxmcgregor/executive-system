---
name: start
description: Daily entry point - orients you on what to work on today
---

# /start

This skill has two modes:

1. **Onboarding mode** -- when `ONBOARDING.md` contains any unchecked items (`- [ ]`)
2. **Operating mode** -- when all items in `ONBOARDING.md` are checked (`- [x]`)

**Detection:** Read `ONBOARDING.md`. If any line matches `- [ ]`, enter onboarding mode. Otherwise, enter operating mode.

---

## Onboarding Mode

Onboarding has 7 phases: Setup (Step 0, invisible to the user) plus Steps 1-6. Each step corresponds to a checkbox in `ONBOARDING.md`. When the user runs `/start` (or sends any message while unchecked items remain), find the first unchecked item and execute that step.

### Discovery Approach (applies to ALL onboarding steps)

Do not take the user's first answer and immediately write the file. Run discovery first:

1. **Ask the opening question** for the step.
2. **Follow up.** Ask 2-3 clarifying or deepening questions based on what they said. Dig into specifics. If they gave a short answer, ask targeted follow-ups. If they gave a long answer, reflect back what you heard and ask what's missing.
3. **Offer multiple choice when helpful.** If the user seems stuck or gives vague answers, offer options to react to (e.g., "Which of these resonates most: A, B, or C?"). This speeds things up without sacrificing depth.
4. **Confirm before writing.** Before generating the file, summarize what you heard back to them: "Here's what I'm hearing -- [summary]. Anything to add or change?" Only write the file after they confirm.
5. **Check they're done.** After writing, explicitly ask: "Anything else to add to this section, or are we good to move on?"

The goal is a robust, accurate document -- not speed. Two extra questions now save a rewrite later.

### After completing each step:
1. Check it off in `ONBOARDING.md` (change `- [ ]` to `- [x]`)
2. Ask: "Anything else for this section, or ready for the next step?"

If they stop, the next `/start` picks up at the next unchecked item. No guilt, no pressure.

---

### Step 0: Bootstrap (Setup)

If the "Setup" item in `ONBOARDING.md` is unchecked, perform these actions before proceeding. Steps 1-3 are silent (no user-facing output). Steps 4-6 are user-facing.

#### 1. Skills Installation (silent)

Copy skill directories from this repo's `skills/` to `~/.claude/skills/`. If `~/.claude/skills/` already exists, copy individual skill directories into it -- do not replace the whole folder.

If the copy fails, surface a fallback command after the greeting (Step 4):

> I couldn't install the skills automatically. Run this command and we'll continue:
> `mkdir -p ~/.claude/skills && cp -r skills/* ~/.claude/skills/`

After the user runs it, verify the skills installed by checking that `~/.claude/skills/start/SKILL.md` exists. If it doesn't, ask the user to try again or troubleshoot.

#### 2. Directory Verification (silent)

Confirm all repo directories exist. Create any that are missing:
- `goals/`
- `indicators/`
- `experiments/`
- `plans/`
- `backlog/`
- `board/`
- `reviews/weekly/`
- `reviews/board/`
- `logs/build/`
- `logs/journal/`
- `research/`
- `projects/`

#### 3. Git (silent)

If git is already initialized, leave it alone. If not, do nothing. Git is not required. If the user later enables auto-commit, Claude initializes git at that point.

#### 4. Greet the User

This is the first thing the user sees. Explain what the system is and what they're about to do. Keep it welcoming but concise:

> This is your executive system -- a structured way to stay aligned between what you're building toward and what you do each day. It handles goal-setting, weekly accountability, and monthly strategic reviews.
>
> We'll set up your system through a conversation. There are 6 steps after this setup -- Vision, Values, Profile, Board, Goals, and a first Board Meeting. Each takes 5-15 minutes. You can stop after any step and pick up next time.

If skills installation failed in Step 1, surface the fallback command here, after the greeting.

#### 5. Auto-Commit Preference

After the greeting, ask:

> "One quick preference before we start: want me to automatically save a snapshot of your progress at the end of each session? (This uses git -- you can change this anytime.)"

Store the answer in `config.md`:
- Yes: `Enabled: yes`
- No: `Enabled: no`

Default is no.

#### 6. Check Off and Continue

Change the "Setup" line in `ONBOARDING.md` from `- [ ]` to `- [x]`. Ask if the user wants to continue to Step 1.

#### Failure Handling

- **Skills copy fails:** Surface the fallback command (shown above) after the greeting. Verify installation before proceeding. If still failing, continue with onboarding -- the skills exist in the repo's `skills/` directory and Claude can read them directly; slash commands just won't work until installation succeeds.
- **Permission issues:** Explain in plain language, offer the fix.
- **No git:** System works fine without it. Never block on git.

---

### Step 1: Vision

**Why (say this to the user):**

> Everything in this system flows from your vision. Goals, experiments, daily decisions -- they all filter through the life you're building toward. This doesn't need to be polished or certain. It's a direction, not a contract. And it can change -- we revisit it periodically.

**What to extract:**
- The end-state life (day-to-day reality, not abstract aspirations)
- Key dimensions: work, location, relationships, finances, time
- The path from here to there (high-level phases)
- What it's really about (the deeper motivation)

**How to ask:**

Open with:

> "Describe the life you're building toward. Not a business plan -- the actual life. What does a regular day look like when everything is working the way you want?"

**Follow-up strategy:**

If the user writes a lot, ask sharpening follow-ups: "You mentioned X -- say more about that." "What does the financial side look like?" "What's the timeline in your head?"

If they're brief, break it down with targeted questions:
- "What does your morning look like?"
- "Are you working for yourself or someone else?"
- "Where are you?"
- "What's the financial picture?"
- "Who's around?"

If they seem stuck, offer multiple choice: "Is this more about freedom and independence, building something meaningful, financial security, or something else?"

Ask at least 2-3 follow-up questions before writing. Don't rush to the file.

**Output:** Summarize what you heard, confirm with the user, then write `VISION.md`. Use natural sections that fit what they described -- not a rigid template.

**Then:** Check off "Vision" in `ONBOARDING.md`. Ask if anything's missing or if they're ready to move on.

---

### Step 2: Values & Principles

**Why (say this to the user):**

> Values determine which goals are worth pursuing. Principles determine how you pursue them. When you're torn between two options or deciding how to spend your time, these are the tie-breakers. The system uses them as filters at every level.

**What to extract:**
- 3-5 core values (what matters most)
- 3-5 operating principles (how the user wants to work)

**How to ask:**

> "What matters most to you? Think about the times you've felt most aligned -- what was present? And the times you've felt most off -- what was missing?"

If the user struggles with the open-ended question, offer categories to react to:

> "Here are some common values people orient around -- which pull you, and which don't matter much? Relationships, health, freedom, achievement, creativity, security, adventure, impact, autonomy, mastery, service, growth."

**Follow-up strategy:**

For each value they name, dig in: "When you say freedom, what does that mean specifically for you? Freedom from what?" "You mentioned craft -- what does that look like when it's present vs. absent?"

After values, move to principles:

> "How do you want to operate? What rules do you hold yourself to? Think about the times things went well -- what habits or disciplines were in play?"

If they're brief on principles, offer examples to react to: "Some people operate by 'ship fast, fix later.' Others by 'measure twice, cut once.' Some prioritize consistency, others intensity. What's your style?"

Ask at least 2-3 follow-up questions across values and principles before writing.

**Output:** Summarize what you heard, confirm, then write `VALUES.md` with values and principles clearly separated.

**Then:** Check off "Values & Principles" in `ONBOARDING.md`. Ask if anything's missing or if they're ready to move on.

---

### Step 3: Profile

**Why (say this to the user):**

> The more this system understands about how you're wired, the better it works with you instead of against you. This helps calibrate how goals are framed, how reviews are delivered, and what patterns to watch for. Think of it like giving the system your user manual.

**Primary method: Structured self-report interview.** Ask these questions one or two at a time (not all at once). Follow up on interesting answers before moving to the next question. Adapt based on conversation flow -- skip questions already covered.

Core questions:
- "How do you work best? Morning or night? Long sessions or short bursts?"
- "What drains your energy? What charges it?"
- "When you've failed at something in the past, what was usually the reason? Lost interest? Got busy? Didn't know how to finish?"
- "How do you like to receive feedback? Direct and blunt, or softer?"
- "What are you naturally good at? What do people come to you for?"
- "What's your current situation? Job, time constraints, resources?"

**Follow-up strategy:** The failure modes question is the most important one. Dig in. If they say "I lose interest," ask: "At what point? Early on, or when things get close to done?" If they say "I get busy," ask: "Busy with new things, or busy with obligations?" Offer multiple choice if helpful: "When a project stalls, is it usually because (a) something shinier appeared, (b) you hit a hard part and avoided it, (c) the finish line felt unclear, or (d) something else?"

**What to build in `PROFILE.md`:**
- Work style (chronotype, focus patterns, energy management)
- Strengths
- Known failure modes (derived from self-report)
- Communication preferences
- Current situation (job, constraints, resources)
- Assessment data section (empty placeholder, populated later if provided)

**Output:** Summarize what you heard, confirm, then write `PROFILE.md`.

**AFTER writing PROFILE.md -- personality assessment recommendation (MANDATORY):**

Do NOT check off the Profile step or move to Board Members until you have presented this. This is a separate beat in the conversation, not a footnote at the end of the interview.

After saving the profile, say:

> "Profile saved. Before we move on -- one thing that makes a real difference to how well this system works for you.
>
> Everything in this system -- how I frame feedback, what patterns I watch for, how I run your reviews and board meetings -- calibrates off your profile. The richer the profile, the better it all works. The interview we just did is a solid start, but personality assessment data makes the system significantly sharper. It's the single biggest upgrade you can make.
>
> Two free tests I'd recommend:
> - **Big Five** (most useful): https://bigfive-test.com -- completely free, open source, no account needed. ~10 minutes.
> - **Enneagram**: https://www.truity.com/test/enneagram-personality-test -- free basic results (scores for all 9 types). Ignore the premium upsell.
>
> You don't have to do these now. Whenever you have a spare 20 minutes, take one (or both), paste the results into a conversation, and I'll update your profile automatically. If you've already taken assessments before (MBTI, StrengthsFinder, DISC, anything), share those anytime too."

Wait for the user to acknowledge before proceeding.

**Then:** Check off "Profile" in `ONBOARDING.md`. Ask if anything's missing or if they're ready to move on.

---

### Step 4: Board Members

**Why (say this to the user):**

> The board is a group of perspectives that challenge your thinking during monthly strategic reviews. The system comes with 8 default lenses -- ways of thinking about decisions. You can keep them as-is, replace them with specific people you admire, or do a mix.

**Default lenses:**

| Lens | Perspective |
|---|---|
| Rationality | Clear thinking, inversion, avoiding stupidity |
| Leverage | Compounding, asymmetric bets, force multipliers |
| Sustainability | Pace, energy, long-game thinking |
| Elimination | What to stop, what to say no to, simplification |
| Speed | Bias to action, shipping, reducing cycle time |
| Learning | Pattern recognition, feedback loops, adaptation |
| Visibility | Distribution, positioning, being findable |
| Positioning | Differentiation, strategy, competitive awareness |

**How to ask:**

> "The system has 8 default thinking lenses that challenge your decisions from different angles. You can also replace any of these with specific people -- public figures, mentors, authors, family members, fictional characters. Want to see the defaults, or do you have people in mind?"

If the user names people:
- For public figures, use training knowledge to build the board member file.
- For personal contacts or obscure figures, ask: "Tell me about how they think. What would they push back on? What would they encourage?"

**After each person or batch of people, explicitly ask:** "Anyone else you want on the board, or are we good with these?" Do not assume they're done after the first answer. Keep the door open until they confirm.

Constraints:
- Minimum: 4 board members
- Maximum: 8
- Changeable anytime

**Output:** Write or update board member files in `board/`. Each file follows the board member schema from `CLAUDE.md`:

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

If the user keeps defaults, confirm the 8 files already exist in `board/` and are populated. If any are missing, create them.

**Then:** Check off "Board Members" in `ONBOARDING.md`. Ask if they want to continue or stop for now.

---

### Step 5: Current Situation & Goals

**Why (say this to the user):**

> Now that the system knows who you are and where you're going, we need to know where you are right now and what you're aiming for in the near term. Goals should be things within your control -- "write 10 blog posts" not "get 1000 readers." 2-3 per quarter. Deliberately achievable.

**What to extract:**
- Current situation snapshot (update `PROFILE.md` if new information surfaces)
- 2-3 quarterly goals (controllable, measurable)
- Indicators to watch (not controllable, but informative)
- Any active experiments or projects

**How to ask:**

Start with situation if not already covered in Step 3:

> "What are you working on right now? What's the biggest thing you're trying to make happen?"

Then move to goals:

> "For this quarter, what 2-3 things would make you feel like you made real progress? Remember -- these should be things you can control."

Then indicators:

> "What numbers or signals would tell you things are working, even though you can't control them directly? Revenue, followers, downloads, responses -- anything you'd want to track."

Then experiments/projects:

> "Are you running any experiments or active projects right now? Things you're testing or building?"

**Output:**
- Write `goals/YYYY-QX.md` using the goals schema from `CLAUDE.md` (determine the current quarter from today's date)
- Write `indicators/YYYY-QX.md` using the indicators schema from `CLAUDE.md`
- If experiments are mentioned, create files in `experiments/` using the experiment schema from `CLAUDE.md`
- Update `PROFILE.md` with any new situational information

**Then:** Check off "Current Situation & Goals" in `ONBOARDING.md`. Ask if they want to continue or stop for now.

---

### Step 6: First Board Meeting

**Why (say this to the user):**

> The board meeting is the monthly heartbeat of this system. We're going to run a short version now to validate your goals, get the board's perspective, and make sure everything is aligned before you start.

**What happens:**

Run an abbreviated board meeting. This is the first one, so skip sections that require history:
- **Skip:** Previous Meeting Review (no prior meeting)
- **Skip:** Pattern Review (no weekly reviews yet)

**Do:**
1. Summarize the goals and current situation for context.
2. Have each board lens/member weigh in on the goals and situation. Each perspective should offer one concrete observation or question -- not a monologue.
3. Let the user react and adjust. This is conversational, not a report.
4. Ask the user to commit to the monthly behaviors they'll maintain to hit their goals.

**Output:**
- Write `reviews/board/YYYY-MM-DD.md` using the board meeting schema from `CLAUDE.md`
- Check off "First Board Meeting" in `ONBOARDING.md`

At this point, all items in `ONBOARDING.md` should be checked. Congratulate the user briefly and present the system:

> Your system is set up. Here's the habit loop:
>
> 1. **`/start`** -- begin each work session (2-3 min)
> 2. **`/log`** -- end each work session (1-2 min)
> 3. **`/journal`** -- explore what you're thinking (aim for 1-2x per week -- this gives the system unfiltered insight into how you're actually feeling about the work)
> 4. **`/weekly-review`** -- Fridays (5-10 min)
> 5. **`/board-meeting`** -- first Friday of each month (30-60 min)
>
> `/capture` saves ideas to the backlog anytime. Run `/how-to-use` for the full guide on why each piece matters.

---

## Operating Mode

Used when all items in `ONBOARDING.md` are checked. This is the normal daily flow.

### 1. Read Current State (silently, before responding)

- `goals/` -- find the current quarter's goals file
- `experiments/` -- active experiments and their status
- `plans/` -- active plans with checkbox progress (look for unchecked items and stalled phases)
- `reviews/board/` -- most recent board meeting (read the **Commitments** and **Direction** sections). These define the priorities for the current month.
- `logs/build/` -- last 3-5 build logs (most recent)
- `reviews/weekly/` -- most recent weekly review. **This is the freshest status source.** For each item in the board's commitments, check the weekly review for current status. If the weekly review marks something complete, treat it as complete regardless of the board file's wording. The board defines priorities; the weekly review tracks reality.
- Current date -- check if weekly review is due (Fridays), board meeting due (first Friday of month)
- `PROFILE.md` -- read for chronotype, failure modes, communication preferences to calibrate the session

### 2. Present the Landscape

- Active goals and their current status (how far along, what's next)
- Any experiments approaching evaluation dates
- What was worked on recently (from build logs)
- Any flags from the last weekly review
- Open loops or stalled items

### 3. Surface Options (Prioritized)

List 2-4 concrete options based on current goals, experiments, and board commitments.

**Prioritize using the leverage filter:**

- **High leverage (compounding):** Things that keep producing value after the effort stops -- systems, automation, assets, tools. Surface these first.
- **Medium leverage (momentum):** Active plan phases, deadlines, experiment milestones -- time-sensitive but not compounding.
- **Lower leverage (maintenance):** Routine tasks -- necessary but not compounding. Surface later.

Include a one-line reason for the top recommendation.

### 4. Agree on Focus

The user picks what to work on. Confirm the session's focus. If the user brings up a new idea not in current goals, gently note it and suggest `/capture` instead.

---

### Flags to Surface

- **Weekly review overdue:** "It's Friday (or past Friday) and no weekly review has been logged this week."
- **Board meeting due:** First Friday of the month (or past it) with no board meeting logged this month. "Board meeting is due. Run `/board-meeting` when ready."
- **Experiment approaching evaluation:** "The [experiment] hits its minimum runway on [date]."
- **Stalled project:** "No build log entries mentioning [project] in [N] days."
- **Shiny object detection:** If the user starts talking about a new project not in goals/experiments, don't just flag it -- diagnose it. Ask: "Is the current work feeling predictable, or are you seeing a genuine opportunity?" If stimulation-seeking, suggest reframing current work. If genuine opportunity, suggest `/capture` for board evaluation.
- **Plan avoidance:** Active plan checkboxes not progressing in build logs.
- **Plan phase readiness:** If a plan's current phase prerequisites are met, surface the next actions.
- **Journal nudge:** If no journal entries exist in the past 7 days, suggest it once (not every session): "It's been a while since your last journal entry. If anything's brewing -- a frustration, a decision, an idea -- `/journal` is a good place to work through it."

**Personality-aware framing:** Read `PROFILE.md` for chronotype, failure modes, and communication preferences. Adapt how you present options:
- If the user works best in the morning, surface deep/creative work first
- If failure modes include procrastination, frame urgent items clearly
- If communication preferences say direct, be direct. If they prefer questions, use questions.

---

### Empty-State Branches

Handle missing data gracefully:

- **No goals:** "You haven't set goals yet. Want to do that now, or wait for your first board meeting?"
- **No build logs:** Present goals and suggest starting with one.
- **No experiments:** Skip experiment flags entirely.
- **No plans:** Skip plan progress section.
- **No weekly review history:** Skip "flags from last review" section.
- **No board meeting history:** Skip "board commitments" section.

---

### Tone

- Efficient, not ceremonial. This should take 2-3 minutes.
- Present information, don't lecture.
- The user is the decision maker -- show the landscape, let them choose.
- All flags are data, not judgments. "Build logs show..." not "You failed to..."
- Adapt to `PROFILE.md` communication preferences. If no profile exists, default to direct and concise.

### Produces

Nothing written. Just direction for the session.
