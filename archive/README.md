# Archive

Completed and abandoned documents, preserved for reference and kept out of the hot path —
the files `/start` and routed agents read every session.

- **Structure mirrors the repo.** Archived plans live in `archive/plans/`, past-quarter goals
  in `archive/goals/`, old reviews in `archive/reviews/`, and so on.
- **Nothing here is loaded by default.** Retrieve via direct read or `git log` / `git grep`.
- **State-file *history* is NOT archived here** — it lives in `logs/build/` and git. Only finished
  or abandoned *documents* move here; the state layer is overwritten in place, not archived.
- **Quarter-boundary habit:** at each quarter close, move the prior quarter's `goals/` and
  `indicators/` files here so the live directories only ever hold the current quarter.

When a plan, experiment, or spec is done or abandoned, move it under the matching `archive/`
subdirectory rather than deleting it or leaving it to clutter the active folder.
