# 1. Record architecture decisions

**Status:** Accepted

## Context

This repo has already gone through several structural changes — converting
plain persona prompts into Claude Code subagents, removing a subagent that
turned out not to be able to function as one, consolidating a duplicated
directory structure into a single source of truth. Each of those decisions
had real reasoning behind it that currently only lives in commit messages
and PR descriptions, which are easy to miss when skimming the repo later.

## Decision

We will keep lightweight Architecture Decision Records in `docs/adr/`, one
file per decision, using the format described in `docs/adr/README.md`.

## Consequences

- Structural decisions get a stable, discoverable home instead of being
  scattered across commit history.
- Adds a small amount of overhead to decisions that warrant it — not every
  change needs a record (see `docs/adr/README.md` for the threshold).
