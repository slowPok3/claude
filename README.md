# claude
Claude Agents and related

## Using this repo as a project template

This repo doubles as a **Claude Code project template**. `.claude/agents/` at the repo root contains five ready-to-use subagents:

- `performance-reviewer` — algorithmic complexity, memory, I/O, concurrency, DB query review
- `security-reviewer` — OWASP-aligned vulnerability review
- `benchmark-runner` — designs and runs rigorous performance benchmarks
- `test-runner` — writes/reviews unit test suites (pytest, Jest/Vitest, JUnit, Pester, RSpec, Go, .NET)
- `stress-tester` — load/stress/soak/breakpoint testing

Click **"Use this template"** on GitHub to start a new project with these subagents already active — Claude Code auto-discovers `.claude/agents/*.md` on open, no setup required. They'll auto-invoke based on their `description`, or you can call one explicitly (e.g. "use the security-reviewer agent").

The canonical, documented source for these agents (with full rationale and catalog) lives in [`agent-architecture/code-review-agents/`](./agent-architecture/code-review-agents/) — `.claude/agents/` holds working copies for direct use. If you edit an agent's behavior, update both locations.
