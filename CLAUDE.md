# CLAUDE.md

Guidance for Claude Code when working in this repository or in any project created from it as a template.

## What this repo is

Not a software project — there is no source code, build system, package manifest, linter, or test suite. It's a library of AI agent system prompts. "Development" here means editing/authoring Markdown agent files and keeping `README.md` and `CHANGELOG.md` in sync with them.

`.claude/agents/` is the single source of truth for every agent, both as a live Claude Code subagent (frontmatter + prompt) and as the canonical copy of the prompt text for use in other AI tools (see root `README.md`'s "Using these with other AI platforms"). There is no separate documentation-only copy elsewhere — don't recreate one; edit the file in `.claude/agents/` directly.

Two families of subagent live here:

- **Domain architects** (`python-architect`, `java-architect`, `powershell-architect`, `ansible-architect`, `gitlab-architect`, `powerbi-architect`, `icam-architect`, `pingidentity-architect`, `sailpoint-architect`, `radianlogic-architect`) — generate and review technology-specific solutions.
- **Code review specialists** (`performance-reviewer`, `security-reviewer`, `benchmark-runner`, `test-runner`, `stress-tester`) — language-agnostic, review-only, applied consistently regardless of tech stack.

There is no `principal-solution-architect` subagent — that role isn't needed. See "Acting as the orchestrator" below for why, and `agent-architecture/Principal-Solution-Architect.md` for the persona this replaces (kept for use in tools without native subagent orchestration).

## Repository structure

```
.claude/agents/                         # single source of truth — all 15 subagents
agent-architecture/
├── Principal-Solution-Architect.md     # cross-platform orchestrator persona, not a Claude Code subagent
└── shared-standards/                   # cross-agent conventions
    ├── coding-style-guide.md           # populated
    ├── il5-security-baseline.md        # empty placeholder — not yet written
    └── mermaid-patterns.md             # empty placeholder — not yet written
CLAUDE.md                               # this file
CHANGELOG.md                            # version history
README.md                               # catalog/index of agents, usage instructions
```

## Acting as the orchestrator

When a request spans multiple domains (e.g. "design a GitLab pipeline that deploys a Python service behind PingFederate auth"), you — the main Claude Code session — are the orchestrator. Do not look for or invoke a meta-architect subagent to do this; orchestration is your job natively, and it's exactly why `principal-solution-architect` was deliberately not installed as a subagent (a subagent cannot invoke other subagents, so a meta-orchestrator subagent would have no way to actually delegate):

1. **Decompose** the request into the domains it actually touches. Don't invoke a domain architect for a domain the request doesn't need.
2. **Delegate** to the matching subagent(s) for anything domain-specific and substantial. Run independent domains in parallel (e.g. the GitLab pipeline and the PingFederate config don't depend on each other — dispatch both at once); run dependent ones sequentially (e.g. the Python service's interface needs to exist before the pipeline that deploys it is finalized).
3. **Synthesize, don't repeat.** If a subagent already produced code or a full explanation directly, your follow-up should summarize how its output fits the broader design — not reproduce the code or restate the explanation. Only surface a subagent's raw output yourself if it ran silently (no direct output to the user).
4. **Reconcile conflicts** between subagent outputs before presenting a combined result — e.g. if one architect assumes synchronous calls and another assumes an async queue at the same boundary, resolve it rather than passing the contradiction through.

## Standards every agent (and you) should enforce

These apply whether you're writing code directly or reviewing/synthesizing a subagent's output:

- **No hallucination.** Never invent an API, cmdlet, library behavior, or product feature. State uncertainty explicitly and verify via web search rather than guessing.
- **No hardcoded secrets.** Environment variables, vaults, or platform secret managers only.
- **No real PII/PHI.** Synthetic data only, in examples and fixtures alike.
- **Least privilege** by default in any access-control or IAM design.
- **Robust error handling.** Actionable logging (what failed, why, context) and non-zero exit on critical failure — no silent swallowing.
- **Modern, non-deprecated tooling.** Prefer current SDKs/modules over legacy ones (e.g. Microsoft Graph over deprecated AzureAD/MSOnline) unless a codebase's existing convention says otherwise — match what's already there before introducing something new.
- **Language/tool agnosticism.** Don't default to a familiar stack when another is the better fit for the task or already established in the repo you're working in.

Cross-cutting per-language specifics already defined in `agent-architecture/shared-standards/coding-style-guide.md`: PowerShell (`[CmdletBinding()]`, approved verbs, modern Graph/Az modules over deprecated AzureAD/MSOnline), Python (PEP 8, type hints, venv/requirements.txt), Java (modern language features, Spring Boot default, Maven/Gradle), GitLab CI/CD (explicit `lint/test/build/security_scan/deploy` stages, hardened minimal images, SAST + dependency scanning). Check this file before duplicating a rule per-agent.

## When to reach for a domain architect vs. a review agent

Domain architects and review agents overlap in topic (e.g. `python-architect` has its own performance/security guidance) but not in purpose:

- Use a **domain architect** for end-to-end, technology-specific design or implementation work.
- Use a **review agent** when you want the same review checklist (performance, security, tests, benchmarks, load behavior) applied consistently regardless of which language or platform the code happens to be in.

## Conventions when authoring/editing an agent file

Every agent file in `.claude/agents/` follows the same shape — match it when adding a new one or editing an existing one:

1. **YAML frontmatter**: `name` (matches the filename, kebab-case), `description` (what the agent does + when Claude Code should auto-invoke it — this is what auto-triggering matches against, so be specific), `tools` (scoped to what the agent actually needs — read-only reviewers get `Read, Grep, Glob`; agents that execute code also get `Bash`/`Write`/`Edit`), `model: inherit`.
2. **Title + emoji header** — each agent has a distinct emoji used consistently in headers throughout the file.
3. **Role Definition** section stating the persona's mission and expertise areas.
4. **Zero Hallucination Policy** — near-universal: never invent APIs/cmdlets/features; explicitly say "I don't know" / "I cannot verify this based on available data" when uncertain, and prefer verifying via web search over guessing.
5. **Core Directives & Constraints**, frequently expressed as a `| Principle | Execution Strategy |` markdown table.
6. **Domain-specific standards** or **review checklist** (naming conventions, anti-patterns, IL5-specific security/compliance mandates where relevant).
7. **Output format** section describing exactly how the agent should structure its response.
8. **Version** footer (`**Version:** X.Y.Z`).

## Keeping the docs in sync

When adding a new agent or materially changing an existing one:
- Add/update its entry in the appropriate table in `README.md`.
- Add a version entry for it in `CHANGELOG.md` (this repo tracks a semver per individual agent, separate from the repo's overall version).

## Known quirks

- `.gitignore` does not contain ignore patterns — it currently holds a stray PowerShell snippet (`Set-Location ...; git status`). Be aware of this if editing it; don't assume it's doing normal gitignore work.
- `agent-architecture/shared-standards/il5-security-baseline.md` and `mermaid-patterns.md` are intentionally empty placeholders, not accidentally-blank files.
