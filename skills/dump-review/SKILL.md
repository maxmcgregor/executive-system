---
name: dump-review
description: Periodic cross-corpus synthesis of "the dump" -- mines research, ideas, journals, and reviews for the persistent signal through the noise, surfaces threads the user can't see themselves, and mirrors intention against behavior. On-demand (especially at "what do I do next?" moments) or a few times a year.
---

# /dump-review -- Find the Signal Through the Noise

Think of your **"dump"**: everything on the internet and in your own head that has inspired you or
piqued your interest, scattered across several piles. This skill reads the whole pile at once,
periodically, and finds the **persistent signal through the noise** -- including threads the user
can't see themselves -- then holds those threads up against what their behavior actually did.

It runs on-demand (especially at a "what do I do next? / I'm at a fork" inflection) or on a roughly
four-month heartbeat.

**What this is NOT:**
- Not a capture tool. `/capture` and `/journal` collect the raw material; this synthesizes it.
- Not the board's monthly `IDEAS.md` triage -- that is shallower, monthly, per-item routing. This is
  deeper, a few times a year, cross-corpus, theme-level.

The lens is **work and personal, braided.** Someone's inner life and their strategic direction aren't
separable, and the value is in seeing them together.

---

## The three jobs (in order of value)

1. **Surface the invisible.** Cluster semantically, by *meaning*, not keywords. You are expected to
   make inferential and even creative leaps to name threads the user would not name themselves. The
   whole value is what they can't see on their own. Lead with these.

2. **Weight by persistence.** A theme recurring across **months and multiple piles** is signal; a
   one-week blip is noise. A theme's strength = **time-span of recurrence x cross-corpus spread** --
   NOT raw count inside a single burst. If something was on their radar for a week and never again,
   that is weak signal no matter how intense that week was.

3. **Mirror intention against behavior.** For each strong intention-thread, check the build logs: is
   the user *acting* on it, or just *circling* it in their thinking? Name the alignments and the
   divergences plainly. Lives change through action, not ideas -- if someone wants a certain life,
   their behavior should show it.

---

## The corpus

### Mined for themes (attention / intention)
- `research/` -- everything that resonated externally.
- `backlog/IDEAS.md` + `backlog/REVIEWED.md` -- raw captures and board-parked ideas.
- `logs/journal/**` -- journal entries (richest inner signal).
- `reviews/weekly/**` + `reviews/board/**` -- where the user has already reflected.

### The behavior mirror (read, NOT mined for themes)
- `logs/build/**` -- what the user actually did. Read at a coarse "where did energy actually go"
  level, used ONLY for the intention-vs-behavior read (job 3). Do not theme-cluster it; do not let
  "what they grinded on" dilute the "what resonated" signal.

Every mined item is timestamped (filename dates, saved-on lines, capture-date headings). Use those
dates to compute persistence -- a thread without dates is a vibe.

### Scale note
Read the corpus directly in-session. If it ever outgrows a single context, fall back to subagents
fanning out by corpus and returning per-corpus theme lists for you to synthesize. Don't reach for that
unless a direct read genuinely won't fit.

---

## Flow (conversation first, document second)

The conversation is where real signal gets separated from your inference. The document is the residue
of the conversation, not a report handed over cold.

1. **Read the pile.** The full corpus every run -- persistence needs the whole history, not just what's
   new. Also read the most recent file in `reviews/dump/` if one exists, for the delta.

2. **Build the internal theme map.** Semantic clusters. For each: score persistence (time-span of
   recurrence) and cross-corpus spread. Run each strong intention-thread against the build-log mirror
   (acting vs. circling).

3. **Present findings in conversation.** Lead with the invisible and surprising, then the persistent
   threads, then the intention-vs-behavior divergences. Be Socratic -- a zoomed-out journal session.
   You bring the inference; the user tells you what's real, what's off, what you're over-reading. Push
   a little; the point is non-obvious truth, not agreeableness. Don't dump the whole map at once.

4. **Converge, then write the document.** Capture where *the conversation* landed, not just your
   pre-conversation map. Preserve the user's words where they spoke them -- raw, unedited.

5. **Downstream stays manual.** At the end, *offer* to capture a provocation as an idea (`/capture`) or
   flag one for the next board meeting. **Never auto-route.** The user decides what a theme means.

---

## The document

**Location:** `reviews/dump/YYYY-MM-DD.md` (create `reviews/dump/` if it doesn't exist). It joins the
review family alongside `reviews/weekly/` and `reviews/board/`.

```markdown
# Dump Review -- YYYY-MM-DD

**Window:** [all-time (first run) | since last run YYYY-MM-DD]
**Corpus:** [rough counts -- e.g. "41 journals, IDEAS + REVIEWED, ~30 research saves, 24 weekly +
4 board reviews; build logs since <date> as mirror"]
**Next due:** YYYY-MM-DD  (run date + 4 months; /start reads this)

## The Invisible
[Threads the user likely can't see themselves. Lead here. Name them boldly -- this is where inference
and creative leaps belong.]

## Persistent Threads
[Ranked by strength. For each: what it is, where it shows up (which piles, over what time-span), the
evidence.]

## Intention vs. Behavior
[Where thinking and doing align. Where they diverge -- "you keep circling X in your thinking; build
logs show little action on it" -- and the reverse.]

## Provocations
[3-5 open questions, not directives. Things to sit with.]

## Delta From Last Run
[Second run onward: what strengthened, what faded, what newly emerged. Omit on the first run. The
delta is itself signal over time.]
```

The **Next due** line is the whole cadence mechanism -- `/start` checks the newest file in
`reviews/dump/` and nudges once that date passes. Nothing else to maintain, and the on-demand path is
always available regardless of the calendar.

---

## Tone

- Honest, exploratory, not a cheerleader. Same frame as the journal and the weekly review: inference
  is welcome, being *evaluated* is not. Present threads as observations, not verdicts.
- This is a thinking session, not a report. The value is in the conversation and the non-obvious
  connections, not the tidiness of the document.
- Everything is soft until the conversation converges. Bring strong inferences; hold them loosely.

## Produces

One markdown file per run at `reviews/dump/YYYY-MM-DD.md`.
