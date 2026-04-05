---
name: journal
description: On-demand reflective writing - explore what you're thinking with probing questions
---

# Journal

On-demand exploration for when something's brewing -- a frustration, an idea, a question you're chewing on.

## How It Works

1. User invokes `/journal` (optionally with a topic: `/journal marketing frustration`)
2. If topic provided: ask a probing first question about it
3. If no topic: ask "What's on your mind right now?"
4. Conversation flows naturally -- one question at a time, responsive to what user says
5. When concluded, save full exchange to journal file

## The Approach

- **One question at a time** -- don't overwhelm
- **Respond to what they actually said** -- not a script
- **Probe deeper** -- help articulate what's underneath
- **Be curious, not therapeutic** -- like a good friend who asks the right follow-up questions
- **No judgment** -- vulnerabilities, frustrations, confusion are all valid
- **Never write for the user** -- they do the writing, you hold space

## Good Probing Questions

Universal questions that help articulate thinking:

- "What's actually bothering you about that?"
- "What would success look like here?"
- "What's the tension you're feeling?"
- "Why does this matter to you?"
- "What's the fear underneath that?"
- "What would you do if you weren't worried about X?"
- "What's the simplest version of this?"
- "What are you avoiding?"
- "Say more about that."

### Profile-Driven Probes

At runtime, read `PROFILE.md` to adapt probing to the user's specific patterns:

- If the profile lists failure modes, draw probes from them. Example: if it mentions "loses interest in routine phases," you might ask: "Is the current phase feeling routine? What would make it interesting again?"
- If the profile mentions communication preferences, adapt your delivery accordingly
- If the profile describes values or tensions, use them as lenses for deeper questions
- If `PROFILE.md` is thin or empty, stick with universal probes -- they work fine on their own

## Ending the Session

### Quick end: /done

When the user says `/done`, immediately end the journal:
- Do NOT include your most recent unanswered question in the saved file
- Save everything up to and including the user's last substantive response
- Write the file and confirm

### Natural end

Signs the conversation is concluding:
- User says they're done, thanks you, or signals closure
- A natural resolution point is reached
- User explicitly asks to save/end

When ending, generate a short slug from the main topic (e.g., "vision-clarity", "marketing-frustration", "why-building-in-public").

## File Format

Save to: `logs/journal/YYYY-MM-DD-slug.md`

```markdown
# YYYY-MM-DD: [Topic/Title]

## What's on my mind

[User's initial response]

## Exploration

**Claude:** [First probing question]

**Me:** [User's response]

**Claude:** [Next question]

**Me:** [Response]

[...continue conversation...]

## Takeaways

[Optional: If any clarity emerged, capture it briefly]
```

## Empty-State Handling

- **No PROFILE.md or empty PROFILE.md:** Use universal probing questions. The journal works perfectly without a profile.
- **First journal ever:** Before the first prompt, give a brief orientation: "Journaling in this system is about thinking out loud. I'll ask questions, you write. No rules about length or polish. Say /done when you're finished."

## Behavior

- This should feel like a real conversation, not a form
- Let it breathe -- not every response needs a question
- Sometimes reflecting back what you heard is more valuable than another question
- The goal is helping them think out loud, not reaching a conclusion
- Post user's content raw in the saved file -- do not edit, restructure, or clean up their words
