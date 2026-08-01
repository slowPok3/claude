# 3. Split the roadmap: template stub vs. this repo's internal backlog

**Status:** Accepted

## Context

`ROADMAP.md` was added to track forward-looking work, cleanly separated from
`CHANGELOG.md`'s historical record. But this repo serves two audiences at
once: it's actively developed as an agent library, *and* it's a Claude Code
project template that other people clone via "Use this template."

A single `ROADMAP.md` conflates them. Its content (add `terraform-architect`,
write `il5-security-baseline.md`, set up CI for the agent files) is entirely
about growing *this* library — meaningless, and actively confusing, noise in
someone else's unrelated project the moment they template this repo.

## Decision

- `docs/internal-roadmap.md` holds this repo's own backlog — everything that
  used to live in `ROADMAP.md`. It's explicitly out of scope for the template
  payload; `README.md`'s "After you use this template" section tells new
  projects to delete it.
- Root `ROADMAP.md` ships empty except for the format, status legend, and
  the "keeping this file honest" instructions — it's the reusable artifact,
  not our leftovers.
- `CLAUDE.md`'s "Tracking the roadmap" section documents the split so it
  doesn't get recombined by accident later.

## Consequences

- Someone using this as a template gets a genuinely clean `ROADMAP.md` to
  start filling in for their own project, instead of inheriting our backlog.
- We still get a real internal tracker for the agent library's own
  development — nothing was lost, it just moved to a file whose name makes
  its scope explicit.
- Two roadmap-shaped files exist now instead of one; `CLAUDE.md` has to keep
  their purposes distinct or this decision quietly erodes.
