# claude
Claude Agents and related

A library of enterprise-grade AI agent system prompts. Every agent lives as a single Markdown file in **[`.claude/agents/`](./.claude/agents/)** — that's the one source of truth, whether you're using it as a Claude Code subagent or pasting its body into another AI tool.

## What's in here

**Code review specialists** (language-agnostic, review-only):
| Agent | Expertise |
|---|---|
| `performance-reviewer` | Algorithmic complexity, memory/allocation, I/O and N+1 detection, concurrency, database query performance |
| `security-reviewer` | OWASP-aligned vulnerability review — injection, broken auth/access control, sensitive data exposure, XXE, XSS/CSRF, SSRF, crypto misuse, dependency risk |
| `benchmark-runner` | Designs and runs rigorous, reproducible performance benchmarks (timeit, JMH, BenchmarkDotNet, criterion, etc.) |
| `test-runner` | Writes/reviews unit test suites across languages (pytest, Jest/Vitest, JUnit, Pester, RSpec, Go `testing`, .NET) |
| `stress-tester` | Load/stress/soak/breakpoint testing (`k6`, `locust`, `pgbench`, etc.), failure-mode analysis |

**Domain architects** (generative, technology-specific design/implementation):
| Agent | Expertise |
|---|---|
| `python-architect` | Enterprise Python, async/concurrency, type safety, pytest |
| `java-architect` | Enterprise Java/Spring Boot, throughput, latency |
| `powershell-architect` | Enterprise PowerShell, M365/Azure module strategy |
| `ansible-architect` | Ansible playbooks/roles, Automation Platform (AAP) |
| `gitlab-architect` | GitLab CI/CD, GitOps, HA/DR, runner fleets |
| `powerbi-architect` | Power BI semantic models, DAX, governance |
| `icam-architect` | Zero Trust / ICAM security architecture |
| `pingidentity-architect` | PingFederate/PingAccess/PingDirectory/PingOne/DaVinci |
| `sailpoint-architect` | IdentityIQ/IdentityNow IGA |
| `radianlogic-architect` | RadianOne FID/ICS/HDAP identity virtualization |

There's topical overlap where a domain architect covers the same ground as a review agent for its language (e.g. `python-architect` has its own performance/security/test guidance). Use a domain architect for end-to-end, technology-specific work; use a review agent when you want the same checklist applied consistently across any language.

## Using these with Claude Code

This repo doubles as a **Claude Code project template**. `.claude/agents/` is auto-discovered by Claude Code on open — no setup required — and root [`CLAUDE.md`](./CLAUDE.md) gives it the orchestration and standards guidance to use them well. Click **"Use this template"** on GitHub to start a new project with all 15 agents already active.

Agents auto-invoke based on their `description` frontmatter, or call one explicitly: "use the security-reviewer agent on this file." Run `/agents` in Claude Code to see everything installed and each agent's tool scope.

There is no `principal-solution-architect` subagent. A Claude Code subagent can't invoke other subagents, so a meta-orchestrator subagent has no way to actually delegate — that job is inherently the main Claude Code session's, and its guidance lives directly in root `CLAUDE.md` instead.

## Using these with other AI platforms

Every file under `.claude/agents/` is plain Markdown: a YAML frontmatter block (metadata Claude Code reads) followed by the actual system prompt. For ChatGPT, a fresh Claude.ai conversation, or any tool without native subagent orchestration:

1. Open the agent's `.md` file
2. Copy everything **after** the closing `---` of the frontmatter (the frontmatter itself is Claude-Code-specific metadata; the prompt body works anywhere)
3. Paste it as a system prompt / custom instructions in your AI tool of choice
4. Start asking questions or requesting code

For cross-domain work in a tool without native orchestration, use **[`agent-architecture/Principal-Solution-Architect.md`](./agent-architecture/Principal-Solution-Architect.md)** as your system prompt — it's a meta-orchestrator persona designed to decompose a request and reason through multiple domains in a single conversation. (This is the one agent that's deliberately *not* in `.claude/agents/`, since Claude Code already does real multi-agent orchestration natively and doesn't need a persona simulating it.)

## Repository structure

```
.claude/agents/                         # single source of truth — all 15 subagents
agent-architecture/
├── Principal-Solution-Architect.md     # cross-platform orchestrator persona (see above)
└── shared-standards/                   # cross-agent conventions referenced when authoring/editing agents
    ├── coding-style-guide.md
    ├── il5-security-baseline.md        # placeholder
    └── mermaid-patterns.md             # placeholder
CLAUDE.md                               # guidance for Claude Code working in/from this repo
CHANGELOG.md                            # version history
README.md                               # this file
```
