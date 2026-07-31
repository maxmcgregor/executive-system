# Initiatives

> Registry of every initiative and the work inside it. **Current truth only** -- overwritten,
> never appended. History lives in `logs/build/` + git.
> Maintained by `/log` (story status) and `/board-meeting` (initiative status).
> Read by `/start` and `/weekly-review`.
> _As of YYYY-MM-DD_

## What this file is for

Goals say what you're committing to this quarter. Plans say how a single effort breaks down.
Neither answers the question you actually ask at the start of a session: **"what's next on X?"**

This file answers it in one read. Every effort gets an ID, every step inside it gets a numbered
ID, and that same ID string appears in three places: the row here, the plan doc, and the build-log
line when the step ships. One grep on the ID assembles the whole paper trail -- idea to plan to
execution to result.

You do not need this on day one. If you're working on exactly one thing, `state/projects.md` and a
plan file are enough. Stand this up when you have **two or more efforts running** and you start
losing track of which one is where.

## How to read this

- An **initiative** is one effort with its own ID: `<area>-<name>` -- e.g. `blog-seo`,
  `app-launch`, `system-cleanup`.
  **Area** = the thing the work operates on. Use your own short slugs and keep them stable: one per
  project, plus `system` for work on this system itself and `cross` for work spanning several.
  Each area gets its OWN initiative for a given kind of work, so their progress is tracked
  independently (`blog-seo` and `app-seo` are two initiatives, not one).
- A **story** is one step inside an initiative: `<initiative>.<n>` -- e.g. `blog-seo.2`.
  The number is the intended sequence, not a priority.
- **Initiative status:** `active` | `parked` | `complete`.
- **Story status:** `todo` | `doing` | `done` | `blocked`.
  `done` means the work is **finished and out in the world** -- built, published, and reachable by
  whoever it's for. Not "the code is written." Not "it's in a branch."
  Whether it's *working* is deliberately NOT a status here. This file answers "is the work done?"
  Results tracking answers "is it working?" -- keep those separate or the registry turns into a
  progress-report and stops being scannable.
- **What's next on an initiative** = the lowest-numbered `todo` story whose depends-on are all
  `done`. That rule makes "what's next" deterministic instead of a judgment call.
- Only **active** initiatives get a story table. Parked and complete ones stay in the index only --
  their detail is in their plan doc and in git.

## Keeping it lean (the rule that makes this survive)

A registry that grows without a shrink rule becomes the thing nobody reads.

- **A `done` row is exactly one line:** ID, story (six words or fewer), `done`, depends-on, a
  pointer, and the ship date. The pointer is the live artifact plus the one doc that holds the
  detail -- **no commit hashes, no test counts, no architecture notes, no war stories.** Those live
  in the build log; grep the story ID to find them. A `done` row longer than one line is a bug.
- **A `todo` / `doing` / `blocked` row gets at most two sentences:** what it is, the next concrete
  action, and what it's waiting on. It collapses to the one-liner the moment it's `done`.
- **The "next on X" pointer is one line,** overwritten each time -- never grown into a list.

## Initiative Index

| ID | Initiative | Area | Status | One-liner | Plan doc |
|----|-----------|------|--------|-----------|----------|
| example-launch | Ship the thing | example | active | Delete this row once you've added your own. | `plans/example.md` |

## example-launch -- stories

| ID | Story | Status | Depends-on | Artifact | Shipped |
|----|-------|--------|-----------|----------|---------|
| example-launch.1 | Pick the scope | done | -- | `plans/example.md` | YYYY-MM-DD |
| example-launch.2 | Build the first version | doing | .1 | The core flow works end to end; next action is wiring the last screen. Waiting on nothing. | |
| example-launch.3 | Put it in front of people | todo | .2 | Announce wherever the audience already is. Gated on `.2` being usable by someone who isn't you. | |

> **Next on example-launch:** `example-launch.2` -- wire the last screen.
