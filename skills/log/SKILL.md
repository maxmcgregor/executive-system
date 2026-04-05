---
name: log
description: End-of-session ritual - logs what you accomplished and checks direction
---

# Daily Build Log

A ritual for when you're done with a work session. Captures what you did, and pivots to journaling if you're getting reflective.

## How It Works

1. **Scan conversation context** for completed work not yet on today's build log
   - Read today's build log (if it exists) to know what's already captured
   - Review the conversation history for: things built, files created/edited, ideas captured, decisions made, problems solved, or any other concrete actions taken
   - Draft suggested log entries as bullet points
2. **Present the suggestion:**
   - Show the suggested bullets: "Based on this session, here's what I'd log: [bullets]"
   - Accept as-is, edit (user types corrections/additions), or skip (don't log anything)
3. **After acceptance or edit**, triage:
   - **Task content** -> save to build log
   - **Reflective content** -> detect it, offer to pivot to journal

## Triage Rules

### Task Content (-> Build Log)
- What was built, shipped, fixed
- Concrete actions taken
- Decisions made
- Problems solved

**Extract as concise bullet points. No emotion, no fluff.**

**Consolidate related work into single bullets.** If multiple steps were part of the same task, log it as one bullet, not four. Use parentheticals for notable details. The build log should read as a list of *outcomes*, not a play-by-play of steps taken to get there.

Example input: "I set up the landing page today, added an email signup form and connected it to the mailing list. Feeling good about how much I got done."

Build log output:
```
- Built landing page with email signup (form, confirmation, mailing list integration)
```

### Reflective Content (-> Journal)
Signs of journaling:
- Feelings ("I'm excited", "frustrated", "pumped")
- Why questions ("why does this matter to me")
- Identity/meaning ("I'm realizing...", "this is who I am")
- Waxing philosophical

**When detected, ask:**
> "Sounds like there's more behind that. Want to journal on it?"

If yes -> Pivot to journal mode (see below)
If no -> Just save the task log, done

## Build Log Format

Save to: `logs/build/YYYY-MM-DD.md`

```markdown
# YYYY-MM-DD

- Task 1
- Task 2
```

Concise. Factual. No narrative.

If appending to existing file, add new bullets under the existing ones.

## Journal Pivot

When the user says yes to journaling:

1. **Don't start fresh** - Use what they already said as the seed
2. **Prompt once** - Ask an open question based on what they shared
3. **Let them write** - They do the writing, you hold space
4. **Prompt again if they continue** - One question at a time
5. **Save when done** - They signal they're finished

**Your role in journal mode:**
- Prompt and probe. Never write for them.
- One question at a time.
- No praise, no therapy-speak.
- Help them articulate what's underneath.

**Good journal prompts:**
- "What's behind that?"
- "Why does this matter to you?"
- "What are you actually realizing?"
- "Say more about that."

**Journal file:**
Save to: `logs/journal/YYYY-MM-DD-<slug>.md`

```markdown
# [Topic/Theme]

[The seed - user's original words that triggered the journal pivot]

---

> First prompt?

[User's exact words, unedited]

> Second prompt?

[User's exact words, unedited]

...
```

**Format:**
1. The seed (original reflective content) for context
2. A `---` divider
3. The dialogue as it happened -- prompts as blockquotes, user's words exactly as typed

No cleaning up, no smoothing, no putting words in their mouth.

---

## Honest Day Check

After saving the build log, evaluate the session's work.

**How:**
1. Read today's full build log (all entries, not just this session)
2. Read current quarter's goals (`goals/`)
3. Assess two dimensions:
   - **Volume:** Did meaningful work happen today, or was it light/distracted?
   - **Direction:** Did the work point toward active goals?

**Output:** One or two sentences. Not a scorecard -- a honest read from a peer.

**Examples:**
- "Honest day. Real work toward your goals."
- "Solid volume but scattered. Fine for one day."
- "Light day. Worth noticing if it's a pattern."
- "Busy day, but most of it was infrastructure, not goal work. The weekly review will catch if this becomes a trend."

**Principles:**
- The goal is permission to stop, not a grade.
- If the work was honest and directional, say so and move on.
- If it was light or off-direction, note it neutrally. Not a lecture -- just information.
- Don't compare to other days. Evaluate this day on its own.
- The bar: "if I do this kind of work most days, I'll get where I'm going."
- Present as data, not judgment.

### Empty-State Branches

- **No goals set:** Still log. Note: "No goals set yet -- build logs are still valuable for your first weekly review."
- **First log ever:** Skip comparison to previous days. Just save and affirm the habit: "First build log. The data starts here."

---

## Git Behavior

Read `config.md` for auto-commit preference.

- **If `Enabled: yes`:** Commit after save with message `Update build log for YYYY-MM-DD`. If the commit fails (no git initialized, merge conflict, etc.), save the file anyway and surface the error as information.
- **If `Enabled: no`:** Just save the file. No git operations.

Do NOT push unless the user asks.

---

## Flow Summary

```
User invokes /log
    |
Scan conversation for completed work
    |
Read today's build log (skip duplicates)
    |
Present suggested bullets
    |
Accept / Edit / Skip
    |
Triage: Tasks -> build log, Reflective -> journal offer
    |
Honest day check
    |
Git commit (if auto-commit enabled)
    |
Done
```
