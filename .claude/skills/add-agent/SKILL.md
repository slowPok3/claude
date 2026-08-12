---
name: add-agent
description: Scaffolds a new agent file for .claude/agents/ — domain architect or code-review specialist — matching this repo's established frontmatter, section shape, and doc-sync checklist. Use when the user asks to add, create, or propose a new Claude Code agent for this repository.
---

# Add Agent

Scaffold a new file in `.claude/agents/` that matches every other agent in this repo, and make sure the surrounding docs (`README.md`, `CHANGELOG.md`) stay in sync in the same change. This skill encodes the conventions already documented in `CLAUDE.md` ("Conventions when authoring/editing an agent file") and `CONTRIBUTING.md` — read those first if anything below is ambiguous.

## 1. Clarify scope before writing anything

Ask (or infer from the request) whichever of these aren't already clear:

- **Name**: kebab-case, must be unique against every existing `name:` in `.claude/agents/*.md`. Check with `grep -h "^name:" .claude/agents/*.md`.
- **Family**: a **domain architect** (generates/designs solutions for one technology — matches the `python-architect`/`gitlab-architect` pattern) or a **code-review specialist** (language-agnostic, review-only — matches `security-reviewer`/`test-runner`).
- **What gap it fills**: check `README.md`'s catalog first. If there's real overlap with an existing agent, that's a signal to extend the existing one instead of adding a new one — flag this rather than silently proceeding.
- **Emoji**: one distinct emoji, not already used by another agent, used consistently through the new file's headers.

If this request came from a GitHub issue opened with the *New agent proposal* template, most of this is already answered there — use it directly instead of re-asking.

## 2. Write the frontmatter

```yaml
---
name: <kebab-case-name>
description: <what it does> + <when Claude Code should auto-invoke it>. Be specific — this is the only field auto-triggering matches against.
tools: <minimum set the agent needs>
model: inherit
version: 1.0.0
---
```

Tool scoping rule of thumb:
- Read-only review agents: `Read, Grep, Glob`
- Agents that execute code or write files: add `Bash`/`Write`/`Edit` as actually needed — don't copy-paste the full list by default.
- Agents that need to verify current external information (product versions, API changes, CVEs): add `WebSearch`.

## 3. Write the body in this exact order

1. **Title + emoji header**, immediately followed by one line: `**Version:** 1.0.0 · **Compatibility:** ... · **Review Cycle:** ...`. This is the *only* place the version number appears in the body — do not also add a bottom "Version & Maintenance" footer or a "Major Changes in vX.X.X" section; that history belongs in `CHANGELOG.md`, not duplicated in the agent file itself.
2. **Role Definition** — the persona's mission and expertise areas, 2-4 sentences.
3. **Zero Hallucination Policy** — near-universal across every agent in this repo: never invent APIs/cmdlets/features; explicitly say "I don't know" / "I cannot verify this based on available data" when uncertain; prefer verifying via web search over guessing.
4. **Core Directives & Constraints** — frequently a `| Principle | Execution Strategy |` markdown table.
5. **Domain-specific standards** (for architects) or **review checklist** (for review specialists) — the substantive content. Check `agent-architecture/shared-standards/coding-style-guide.md` first so you don't re-litigate a cross-cutting rule already established there.
6. **Output format** — describe exactly how the agent should structure its response (a template block or numbered sections works well).

Look at an existing agent of the same family (`.claude/agents/python-architect.md` for an architect, `.claude/agents/security-reviewer.md` for a review specialist) as the structural reference — match its shape, not its content.

## 4. Update the docs in the same change

- **`README.md`**: add a row to the appropriate catalog table (code review specialists vs. domain architects) with a one-line expertise summary.
- **`CHANGELOG.md`**: add an entry under `## [Unreleased]` for the new agent (this repo tracks a semver per individual agent).

Skipping this step is the most common way this repo's docs go stale — don't treat it as optional.

## 5. Verify before handing off

- [ ] `name:` doesn't collide with any existing agent
- [ ] File parses as valid YAML frontmatter followed by Markdown (starts with `---`, frontmatter closed by a second `---`, no stray characters or BOM before it)
- [ ] `description:` states both what the agent does and when it should trigger
- [ ] `tools:` is scoped, not copy-pasted
- [ ] Exactly one version mention in the body (the top-of-file line) plus the frontmatter `version:` field — no third location
- [ ] `README.md` and `CHANGELOG.md` both updated

This matches `CONTRIBUTING.md`'s pre-PR checklist — if you're about to open a PR for this new agent, that file has the full list including the non-agent-file items (no hardcoded secrets, no real PII/PHI in examples).
