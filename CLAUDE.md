# CLAUDE.md

Guidance for Claude Code when working in this repository or in any project created from it as a template.

## What this repo is

A library of Claude Code subagents (`.claude/agents/`) plus their documented, canonical source (`agent-architecture/`). There is no build/lint/test suite — "development" here means editing Markdown persona/subagent files and keeping `agent-architecture/README.md` and `CHANGELOG.md` in sync with them. See `agent-architecture/CLAUDE.md` for the detailed authoring conventions when adding or editing an agent file.

Two families of subagent live here:

- **Domain architects** (`python-architect`, `java-architect`, `powershell-architect`, `ansible-architect`, `gitlab-architect`, `powerbi-architect`, `icam-architect`, `pingidentity-architect`, `sailpoint-architect`, `radianlogic-architect`) — generate and review technology-specific solutions.
- **Code review specialists** (`performance-reviewer`, `security-reviewer`, `benchmark-runner`, `test-runner`, `stress-tester`) — language-agnostic, review-only, applied consistently regardless of tech stack.

There is no `principal-solution-architect` subagent — that role isn't needed. This section replaces it.

## Acting as the orchestrator

When a request spans multiple domains (e.g. "design a GitLab pipeline that deploys a Python service behind PingFederate auth"), you — the main Claude Code session — are the orchestrator. Do not look for or invoke a meta-architect subagent to do this; orchestration is your job natively:

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

## When to reach for a domain architect vs. a review agent

Domain architects and review agents overlap in topic (e.g. `python-architect` has its own performance/security guidance) but not in purpose:

- Use a **domain architect** for end-to-end, technology-specific design or implementation work.
- Use a **review agent** when you want the same review checklist (performance, security, tests, benchmarks, load behavior) applied consistently regardless of which language or platform the code happens to be in.

## Keeping this file honest

If you add, rename, or remove a subagent under `.claude/agents/` or `agent-architecture/`, update the lists above in the same change — this file should never describe an agent roster that doesn't match what's actually installed.
