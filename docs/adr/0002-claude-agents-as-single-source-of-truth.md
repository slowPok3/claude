# 2. `.claude/agents/` as the single source of truth

**Status:** Accepted

## Context

The repo originally held each agent's prompt as a single, documented file
under `agent-architecture/` (`domain-architects/*.md`,
`code-review-agents/*.md`), meant to be copy-pasted as a system prompt into
any AI tool. When this repo was set up to also work as a Claude Code project
template, working copies of the same content were added under `.claude/agents/`
(the path Claude Code auto-discovers), because Claude Code doesn't scan
arbitrary repo paths for subagents.

That left every agent duplicated in two places with no mechanism keeping them
in sync — a real drift risk the moment either copy was edited without the
other.

We also converted `Principal-Solution-Architect.md` to subagent frontmatter
and initially added it to `.claude/agents/` alongside the rest. On review,
this didn't hold up: a Claude Code subagent cannot invoke other subagents, so
the persona's entire "decompose → delegate → synthesize" behavior has no
mechanism to execute when loaded as one. That orchestration role is
inherently the main Claude Code session's job.

## Decision

- `.claude/agents/` is the single source of truth for every agent that
  functions as a Claude Code subagent. The duplicate copies under
  `agent-architecture/domain-architects/` and
  `agent-architecture/code-review-agents/` were deleted.
- `agent-architecture/` now holds only what genuinely can't live in
  `.claude/agents/`: `Principal-Solution-Architect.md` (kept for its original
  use case — pasting as a system prompt into tools without native subagent
  orchestration) and `shared-standards/`.
- The orchestration guidance `Principal-Solution-Architect.md` describes was
  rewritten into root `CLAUDE.md` as direct instructions for the main Claude
  Code session, which is the thing that actually performs multi-agent
  delegation in this repo.
- Root `README.md`, `CLAUDE.md`, and `CHANGELOG.md` (moved from
  `agent-architecture/`) are the canonical docs; there is no second copy of
  the catalog or the authoring conventions.

## Consequences

- No more manual-sync burden between two copies of the same 15 files.
- Using an agent's prompt in a non-Claude-Code tool now means opening the
  file in `.claude/agents/` and copying everything after the frontmatter,
  rather than reading a separately maintained copy.
- `principal-solution-architect` is not available as a Claude Code subagent
  and never will be, by design — anyone looking for it in `.claude/agents/`
  won't find it; `README.md` and `CLAUDE.md` both explain why.
