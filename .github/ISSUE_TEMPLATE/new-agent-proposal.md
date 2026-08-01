---
name: New agent proposal
about: Propose a new domain architect or code-review specialist
title: "[New agent] "
labels: new-agent
---

## Agent name

Proposed `name:` (kebab-case, matches the future filename in `.claude/agents/`):

## Family

- [ ] Domain architect (generates/designs technology-specific solutions)
- [ ] Code review specialist (language-agnostic, review-only)

## What gap does this fill?

Explain what this agent covers that no existing agent does. Check the catalog
in `README.md` first — if there's meaningful overlap with an existing agent,
explain why a new agent is still the right call vs. extending the existing one.

## Proposed `description:`

Draft the frontmatter `description` you'd expect this agent to ship with —
this is what Claude Code auto-triggering matches against, so it should state
both what the agent does and when it should be invoked.

## Proposed `tools:`

What does this agent need? (Read-only reviewers: `Read, Grep, Glob`. Agents
that execute code: add `Bash`/`Write`/`Edit` as needed.)

## Anything else

Prior art, reference docs, or existing prompts this could be based on.
