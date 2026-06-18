# Executive System -- Agent Guide

This is a personal executive system: values, vision, goals, experiments, reviews, and skills that help
the user choose what to work on, reflect, and stay aligned. This guide orients any AI agent (Codex,
Claude Code, or other) on how to read and write the repo. `CLAUDE.md` is the fuller operating manual;
this is the fast map.

## Read Order

1. `state/dashboard.md` -- compact current state. Start every session here.
2. `state/projects.md` -- active project status, phases, next actions.
3. `state/direction.md` -- strategic tracking, live decisions, open questions.
4. `context-map.yaml` -- find the domain that matches today's work; load only what it points to.
5. Domain-specific files, only as needed.

The `state/` files are a **current-truth projection** -- read them at face value. Do not reconstruct
status by re-reading build logs; the state layer is kept current for exactly that reason. (If the
state files are still empty scaffolding, fall back to `goals/` + the latest review + recent build logs
for that session.)

## Directory Map

| Directory | Purpose | Load pattern |
|-----------|---------|-------------|
| `state/` | Pre-computed current truth: dashboard, projects, direction | Always first |
| `goals/` | Quarterly goals (controllable, measurable) | On-demand |
| `indicators/` | Metrics being watched (not controlled) | On-demand |
| `experiments/` | Active experiments with hypotheses and runways | On-demand |
| `plans/` | Active execution plans with checkboxes | On-demand |
| `reviews/weekly/` | Weekly accountability reviews | On-demand |
| `reviews/board/` | Monthly board meeting outputs | On-demand |
| `logs/build/` | Daily build logs (what was done -- the event stream) | On-demand |
| `logs/journal/` | Journal entries (reflections) | Rarely |
| `backlog/` | IDEAS.md (raw), REVIEWED.md (parked), ARCHIVE.md (promoted/killed) | On-demand |
| `board/` | Board member / lens perspective files | During /board-meeting only |
| `research/` | Optional: saved articles, reference material, reusable notes | On-demand |
| `archive/` | Finished/abandoned docs, mirroring the repo structure | Rarely (retrieval only) |
| `projects/` | Optional: active project directories | On-demand by project |
| `skills/` | Claude Code skills (slash commands) | Loaded by the harness |

## Content Tiering

| Tier | Location | Shelf life |
|------|----------|-----------|
| Current truth | `state/*` | Days (overwritten every session as reality changes) |
| Strategic frame | `goals/`, `indicators/`, `experiments/`, `board/` | Quarterly |
| Narrative history | `logs/`, `reviews/`, `plans/` | Permanent but rarely re-read |
| Reusable notes | `research/` (optional) | Months to permanent |

## The Two Records (do not mix them)

- **Event stream** -- `logs/build/*.md` + git. Append-only. The durable history. Write here first.
- **Current-truth projection** -- `state/*.md`. Overwritten, never appended. Read first each session.

When something changes, overwrite the relevant state line with current truth and carry forward only
open items. Anything resolved or historical drops out -- it is already in the build log and git.
**Never write a `Prior:` chain or running narrative into the state files.** That is the one rule that
keeps the hot path small.

## Session Closeout Contract

When `/log` runs at the end of a session:
1. **Write the build log first** -- the append-only record of what happened today.
2. **Update state** -- if priorities, blockers, project phases, goals, experiments, or open questions
   changed, overwrite the relevant `state/*` files to current truth (carry forward open items only).
3. **Capture anything durable** -- a reusable lesson goes to `research/` or a notes file; a new idea
   goes to `backlog/IDEAS.md` via `/capture`.

## System Boundaries

- This repo tracks meta-context (strategy, goals, reviews) -- not project source code.
- Directories under `projects/` may be independent git repos with their own guides.
- Secrets live in project `.env` files, never in this repo.
- `state/` is working state, not historical record. History lives in `logs/` and `reviews/` and git.
