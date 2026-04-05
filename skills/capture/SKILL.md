---
name: capture
description: Quick idea capture to the backlog - no evaluation, just save it
---

# /capture

Quick idea capture. No evaluation, no discussion, no action. Just save it and move on.

---

## Invocation

```
/capture habit tracker app with weekly reflection prompts
```

Or just `/capture` -- prompt the user for the idea if none provided.

---

## Flow

1. Parse the idea from the user's message (or prompt for it if invoked bare)
2. Append to `backlog/IDEAS.md` in this format:

```markdown
- [YYYY-MM-DD] Idea description
```

3. Confirm captured. Done.

---

## Rules

- **No evaluation.** Do not say "that's a great idea" or "that might not work." Just capture it.
- **No discussion.** Unless the user explicitly asks to explore, save and move on.
- **No action.** The idea goes to the parking lot, not to active work.
- **If the user wants to discuss:** "Captured. Want to explore this further, or save it for the board to evaluate?"

---

## Empty-State Handling

- **`backlog/IDEAS.md` missing:** Create it with the header from the schema in `CLAUDE.md`, then append the idea.
- **`backlog/` directory missing:** Create it, then create `IDEAS.md`, then append.

---

## Why This Exists

Ideas are valuable when captured, dangerous when acted on impulsively. This skill separates capture from execution. The board triages `backlog/IDEAS.md` monthly -- ideas get evaluated in context, not in the moment of excitement.
