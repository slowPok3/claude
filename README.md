# claude
Claude Agents and related

## Using this repo as a project template

This repo doubles as a **Claude Code project template**. `.claude/agents/` at the repo root contains 16 ready-to-use subagents:

**Code review specialists (language-agnostic):**
- `performance-reviewer` — algorithmic complexity, memory, I/O, concurrency, DB query review
- `security-reviewer` — OWASP-aligned vulnerability review
- `benchmark-runner` — designs and runs rigorous performance benchmarks
- `test-runner` — writes/reviews unit test suites (pytest, Jest/Vitest, JUnit, Pester, RSpec, Go, .NET)
- `stress-tester` — load/stress/soak/breakpoint testing

**Domain architects (design/generate, technology-specific):**
- `principal-solution-architect` — cross-domain orchestrator, delegates to the architects below
- `python-architect`, `java-architect`, `powershell-architect`, `ansible-architect`, `gitlab-architect`, `powerbi-architect`
- `icam-architect`, `pingidentity-architect`, `sailpoint-architect`, `radianlogic-architect` (identity/IAM platforms)

No `name:` collisions exist between the two groups. There's topical overlap where a domain architect covers the same ground as a code-review agent for its language (e.g. `python-architect` has its own performance/security/test guidance) — use the domain architect for end-to-end language-specific work, and the review agents when you want a consistent checklist applied across any language.

Click **"Use this template"** on GitHub to start a new project with all of these subagents already active — Claude Code auto-discovers `.claude/agents/*.md` on open, no setup required. They'll auto-invoke based on their `description`, or you can call one explicitly (e.g. "use the security-reviewer agent").

The canonical, documented source for these agents (with full rationale and catalog) lives in [`agent-architecture/`](./agent-architecture/) — `.claude/agents/` holds working copies for direct use. If you edit an agent's behavior, update both locations.
