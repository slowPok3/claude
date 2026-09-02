# 4. Add a third agent family: content specialists

**Status:** Accepted

## Context

`CLAUDE.md` has stated "two families of subagent" since this repo's `.claude/agents/` consolidation (ADR 0002): domain architects (generative, technology-specific) and code-review specialists (language-agnostic, review-only). Every agent added since then fit one of those two categories.

Adding `technical-writer` — an agent that writes and improves documentation (READMEs, API references, release notes, migration guides) — doesn't fit either. It's generative, like a domain architect, but it isn't technology-specific: it applies to any codebase regardless of language or stack, the same way the review specialists do. It also isn't a review agent: its job is to produce or improve content, not to find defects in existing code.

Forcing it into an existing category would have made the category boundary meaningless (either "domain architect" stops meaning technology-specific, or "review agent" stops meaning review-only).

## Decision

Add a third family, **content specialists**: language-agnostic and generative, but producing documentation rather than code. `technical-writer` is the first (and, for now, only) member.

Updated everywhere the two-family split was stated as architectural fact: `CLAUDE.md`'s "What this repo is" and "When to reach for..." sections, and `README.md`'s catalog.

## Consequences

- The "two families" framing in `CLAUDE.md` and `README.md` needed updating in multiple places, not just an agent catalog row — this is why it's an ADR and not just a CHANGELOG entry.
- `trim-agents` needed a rule for the new family too (default to keeping `technical-writer`, same reasoning as the review specialists — broadly applicable regardless of stack).
- Future agents that are generative-but-not-code (e.g. a hypothetical `diagram-generator` or `changelog-writer`) now have an obvious home instead of being awkwardly filed as a "domain architect" for a domain that isn't really a technology.
