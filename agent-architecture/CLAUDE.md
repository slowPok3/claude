# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is **not** a software project — there is no source code, build system, package manifest, linter, or test suite. The repository is a curated library of Markdown **system prompts**, each defining an "architect" persona (a specialized system prompt) to be pasted into an AI assistant (Claude, ChatGPT, etc.) so it role-plays as an enterprise subject-matter expert for a given technology domain. All work here is prompt engineering and documentation editing, not code changes.

There are no commands to build, lint, or test. "Development" consists of editing/authoring Markdown files and keeping the cross-referencing docs (`README.md`, `CHANGELOG.md`) in sync.

## Repository structure

```
agent-architecture/
├── Principal-Solution-Architect.md   # Meta-orchestrator prompt (see below)
├── domain-architects/                # One system prompt per technology domain
│   └── <name>-architect.md
├── shared-standards/                 # Cross-domain standards referenced by all architects
│   ├── coding-style-guide.md         # Populated
│   ├── il5-security-baseline.md      # Empty placeholder — not yet written
│   └── mermaid-patterns.md           # Empty placeholder — not yet written
├── README.md                         # Catalog/index of architects, maturity table
└── CHANGELOG.md                      # Per-architect semantic versioning history
```

Git branches: `main` (initial commit only, effectively unused/stale) and `develop` (all active work). Treat `develop` as the working branch unless told otherwise.

## Architecture: how the personas fit together

- **`Principal-Solution-Architect.md`** is the top-level orchestrator persona. It does not do domain-specific work itself — it decomposes a request, delegates to the appropriate domain architect(s), and synthesizes their output. Its "Non-Redundancy Protocol" is a key rule: it must summarize how a sub-agent's output fits the broader architecture rather than repeating code/explanations the sub-agent already gave directly to the user, unless that sub-agent ran silently in the background.
- **`domain-architects/*.md`** are independent, self-contained system prompts, one per technology (Ansible, GitLab, ICAM/Zero Trust, Java, PingIdentity, Power BI, PowerShell, Python, RadianLogic, SailPoint). Each is meant to be used standalone (pasted directly as a system prompt) OR invoked as a sub-agent by the Principal Solution Architect.
- **`shared-standards/*.md`** hold conventions meant to apply across every domain architect (currently only `coding-style-guide.md` has real content; the other two are empty placeholders per the CHANGELOG's "Unreleased" plan). When editing a domain architect's language/security rules, check whether the same rule belongs in `shared-standards/coding-style-guide.md` instead of being duplicated per-file.

## Conventions when authoring/editing an architect prompt

Every domain-architect file follows roughly the same template — match it when adding a new one or editing an existing one:

1. **Title + emoji header** (`# 🐍 Elite Python Architect`, etc.) — each domain has a distinct emoji used consistently in headers throughout the file.
2. **Role Definition / Role Identity** section stating the persona's mission and expertise areas.
3. **Zero Hallucination Policy** — near-universal across files: never invent APIs/cmdlets/features; explicitly say "I don't know" / "I cannot verify this solution based on available data" when uncertain, and prefer verifying via web search over guessing.
4. **Core Directives & Constraints**, frequently expressed as a `| Principle | Execution Strategy |` or `| Guideline | Action Required |` markdown table.
5. **Domain-specific standards** (naming conventions, modern-vs-deprecated module/library guidance, framework defaults, security/compliance mandates — often IL5-specific since this is built for a secure IL5 enterprise environment).

Cross-cutting rules already established in `shared-standards/coding-style-guide.md` (apply when writing/reviewing any architect's code-generation guidance):
- No hardcoded secrets — use env vars / Key Vault / Secrets Manager / masked CI/CD variables.
- No real PII/PHI — synthetic data only.
- Principle of least privilege.
- All generated code must have robust error handling with actionable logging (what failed, why, context) and must exit non-zero on critical failure.
- Per-language specifics already defined: PowerShell (`[CmdletBinding()]`, approved verbs, modern Graph/Az modules over deprecated AzureAD/MSOnline), Python (PEP 8, type hints, venv/requirements.txt), Java (modern language features, Spring Boot default, Maven/Gradle), GitLab CI/CD (explicit `lint/test/build/security_scan/deploy` stages, hardened minimal images, SAST + dependency scanning).

## Keeping the docs in sync

`README.md` and `CHANGELOG.md` are a manually maintained catalog and are currently **behind** the actual `domain-architects/` contents — `ansible-architect.md`, `icam-architect.md`, and `powerBi-architect.md` all exist but are not yet listed in README's structure/maturity table or given a CHANGELOG entry. When adding a new architect or materially changing an existing one:
- Add/update its entry in `README.md` (repository structure tree, domain section with Expertise/Key Features, and the maturity table).
- Add a version entry for it in `CHANGELOG.md` (this repo tracks a semver per individual architect, separate from the repo's overall version).

## Known quirks

- `.gitignore` does not contain ignore patterns — it currently holds a stray PowerShell snippet (`Set-Location ...; git status`). Be aware of this if editing it; don't assume it's doing normal gitignore work.
- `shared-standards/il5-security-baseline.md` and `shared-standards/mermaid-patterns.md` are intentionally empty placeholders (tracked in CHANGELOG's "Unreleased" section), not accidentally-blank files.
