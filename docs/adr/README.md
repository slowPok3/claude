# Architecture Decision Records

This folder records the *why* behind structural decisions in this repo —
things a future contributor (or future us) would otherwise have to
reverse-engineer from commit history.

Not every change needs one. Write an ADR when a decision:

- changes where content lives or how it's organized (e.g. single-source-of-truth choices),
- removes or adds a capability in a way that isn't obvious from the diff alone, or
- was genuinely debated (multiple options considered, one picked for a stated reason).

A typo fix or a new agent that follows the existing template doesn't need one.

## Format

One file per decision, numbered sequentially: `NNNN-short-title.md`. Status is
one of `Proposed`, `Accepted`, `Superseded by NNNN`, or `Deprecated`. Once
accepted, treat the record as historical — don't edit it to match new
decisions; write a new ADR that supersedes it instead.

## Index

| # | Title | Status |
|---|---|---|
| [0001](./0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](./0002-claude-agents-as-single-source-of-truth.md) | `.claude/agents/` as the single source of truth | Accepted |
| [0003](./0003-split-roadmap-template-vs-internal.md) | Split the roadmap: template stub vs. this repo's internal backlog | Accepted |
