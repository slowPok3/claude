## Summary

<!-- What does this PR change and why? -->

## Type of change

- [ ] New agent
- [ ] Edit to an existing agent (behavior, checklist, or accuracy fix)
- [ ] Docs only (README / CLAUDE.md / CHANGELOG / shared-standards)
- [ ] Repo governance / tooling

## Checklist

- [ ] Frontmatter (`name`/`description`/`tools`/`model`) is present and valid on any new or edited agent file
- [ ] `name:` is unique across `.claude/agents/`
- [ ] `description:` states both what the agent does and when it should be invoked
- [ ] `tools:` is scoped to what the agent actually needs
- [ ] No hallucinated APIs/cmdlets/features — verified anything uncertain
- [ ] No hardcoded secrets or real PII/PHI in examples
- [ ] `README.md` catalog and `CHANGELOG.md` updated to match

## Notes for reviewers

<!-- Anything a reviewer should know that isn't obvious from the diff. -->
