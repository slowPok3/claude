---
name: Agent bug report
about: An agent gave incorrect, outdated, or hallucinated guidance
title: "[Bug] "
labels: bug
---

## Which agent

`name:` from the agent's frontmatter (e.g. `python-architect`, `security-reviewer`):

## What it said

Quote or paraphrase the incorrect guidance.

## What's actually correct

What should it have said instead? Include a source (official docs, changelog,
CVE, etc.) if you have one — this repo's Zero Hallucination Policy means we'd
rather cite something than guess.

## Where in the file

If you know it, point at the section of the agent's `.md` file under
`.claude/agents/` that needs to change.

## Impact

- [ ] Would produce insecure code if followed
- [ ] Would produce broken/non-functional code if followed
- [ ] Outdated but not actively harmful (deprecated API, old version assumption)
- [ ] Other
