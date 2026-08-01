# Contributing

Thanks for considering a contribution. This repo is a library of AI agent system prompts — every agent lives as one Markdown file in [`.claude/agents/`](./.claude/agents/), usable both as a Claude Code subagent and as a prompt you paste into other AI tools. There's no build/lint/test suite; "contributing" here means editing or adding Markdown agent files and keeping the docs that reference them in sync.

Read [`CLAUDE.md`](./CLAUDE.md) first — it's the canonical description of the repo's structure, the two agent families (domain architects vs. code review specialists), and the standards every agent enforces (no hallucination, no hardcoded secrets, least privilege, etc). Everything below assumes that context.

## Ways to contribute

- **Fix or improve an existing agent** — sharpen its checklist, correct outdated guidance, tighten its `description` so it auto-triggers more accurately.
- **Propose a new agent** — a new domain architect (a technology not yet covered) or a new review specialist (a review discipline not yet covered). Open an issue first using the *New agent proposal* template so we can agree on scope before you write ~500+ lines of prompt.
- **Improve the shared docs** — `README.md`, `CLAUDE.md`, `CHANGELOG.md`, or `agent-architecture/shared-standards/`.

## Adding or editing an agent file

Every file in `.claude/agents/` follows the same shape (see `CLAUDE.md` → "Conventions when authoring/editing an agent file" for the full spec):

1. YAML frontmatter: `name` (kebab-case, matches the filename), `description` (specific enough that Claude Code auto-invokes it on the right tasks and *not* on the wrong ones), `tools` (scoped to what the agent actually needs — read-only reviewers get `Read, Grep, Glob`; agents that execute code also get `Bash`/`Write`/`Edit`), `model: inherit`.
2. Title + emoji header, used consistently throughout the file.
3. Role Definition, Zero Hallucination Policy, Core Directives & Constraints (usually a `| Principle | Execution Strategy |` table).
4. Domain-specific standards or review checklist.
5. Output format section.
6. `**Version:** X.Y.Z` footer.

Before opening a PR:

- [ ] The file parses as valid YAML frontmatter followed by Markdown (no stray characters before the opening `---`, no BOM).
- [ ] `name:` is unique across every other file in `.claude/agents/`.
- [ ] `description:` states both *what* the agent does and *when* it should be invoked — this is the field Claude Code auto-triggering matches against.
- [ ] `tools:` is the minimum set the agent needs, not a copy-pasted "everything."
- [ ] No hallucinated APIs/cmdlets/features — verify anything you're not certain of.
- [ ] No hardcoded secrets or real PII/PHI anywhere in the examples.
- [ ] `README.md` catalog table and `CHANGELOG.md` are updated in the same PR.

## Reporting a problem with an agent

If an agent gave incorrect, outdated, or hallucinated guidance, open an issue with the *Agent bug report* template — include the agent's name, what it told you, and what's actually correct (with a source if you have one).

## Pull requests

- Keep PRs scoped to one agent or one doc change where practical — easier to review, easier to revert.
- Fill out the PR template's checklist honestly; an unchecked box with a one-line reason is more useful than a box checked without verifying it.
- We don't require CI to pass because there isn't any yet (see the Quality & CI items in the roadmap) — reviewers currently verify frontmatter and content by hand.
