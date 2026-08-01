# 🏗️ Agent Architecture - Enterprise System Prompts

## 📋 Overview

This repository contains a comprehensive collection of **enterprise-grade system prompts** for AI agents specializing in various technical domains. Each prompt is designed to enforce best practices, security standards, and architectural excellence.

---

## 📁 Repository Structure

```
agent-architecture/
├── domain-architects/          # Domain-specific expert system prompts
│   ├── gitlab-architect.md
│   ├── python-architect.md
│   ├── powerShell-architect.md
│   ├── java-architect.md
│   ├── pingidentity-architect.md
│   ├── sailpoint-architect.md
│   └── radianLogic-architect.md
├── code-review-agents/         # Focused code-review specialist system prompts
│   ├── performance-reviewer.md
│   ├── security-reviewer.md
│   ├── benchmark-runner.md
│   ├── test-runner.md
│   └── stress-tester.md
├── shared-standards/           # Cross-domain standards and guidelines
│   ├── coding-style-guide.md
│   ├── il5-security-baseline.md
│   └── mermaid-patterns.md
├── Principal-Solution-Architect.md  # Meta-architect for cross-domain solutions
├── README.md                   # This file
├── CHANGELOG.md               # Version history
└── .gitignore                 # Git ignore rules
```

---

## 🎯 Domain Architects

### DevOps & CI/CD

#### 🏗️ GitLab Architect
**File:** `domain-architects/gitlab-architect.md`

**Expertise:**
- GitLab CI/CD pipeline design and optimization
- GitOps workflows (GitLab Agent, ArgoCD, Flux)
- High Availability (HA) and Disaster Recovery
- Runner fleet management and auto-scaling
- DevSecOps integration (SAST, DAST, dependency scanning)
- Compliance and governance frameworks

**Key Features:**
- Zero hallucination policy
- Version-aware (GitLab 15.0+)
- Tier-specific guidance (CE/Premium/Ultimate)
- Performance optimization patterns
- Comprehensive troubleshooting guides

---

### Programming Languages

#### 🐍 Python Architect
**File:** `domain-architects/python-architect.md`

**Expertise:**
- Enterprise Python development (3.10+)
- Async/await and concurrency patterns
- Type safety and modern Python features
- Performance optimization and profiling
- Security best practices
- Testing with pytest

**Key Features:**
- Strict type hinting requirements
- Modern Python 3.10+ features (pattern matching, union types)
- Comprehensive error handling
- Security-first approach
- CI/CD integration examples

---

#### 💻 PowerShell Architect
**File:** `domain-architects/powerShell-architect.md`

**Expertise:**
- Enterprise PowerShell scripting (7.0+)
- Microsoft 365 and Azure automation
- Module selection strategy (PnP, Graph, Az)
- Performance optimization (runspaces, parallel processing)
- Security and compliance

**Key Features:**
- Strategic module selection guide
- Service-specific examples (12+ M365/Azure services)
- Performance benchmarks
- Deprecation warnings for legacy modules
- Complete coding standards

---

## 🔍 Code Review Agents

Unlike the domain architects above (broad, generative personas for a technology), these are narrow, review-focused specialists — each one inspects existing code for a single class of defect and reports concrete, cited findings rather than generating new solutions.

These files are formatted as **Claude Code subagents** (YAML frontmatter with `name`/`description`/`tools` + the persona body). Drop any of them into `.claude/agents/` (project-level) or `~/.claude/agents/` (user-level, all projects) to make them available in Claude Code — see [Using These as Claude Code Subagents](#-using-these-as-claude-code-subagents) below.

#### 🚀 Performance Reviewer
**File:** `code-review-agents/performance-reviewer.md`

**Expertise:** Algorithmic complexity, memory/allocation patterns, I/O and N+1 query detection, concurrency/parallelism review, database query performance.

#### 🔒 Security Reviewer
**File:** `code-review-agents/security-reviewer.md`

**Expertise:** OWASP-aligned vulnerability review — injection, broken auth/access control, sensitive data exposure, XXE, XSS/CSRF, SSRF, path traversal, cryptography misuse, dependency risk. Aligns with `shared-standards/il5-security-baseline.md`.

#### 📊 Benchmark Runner
**File:** `code-review-agents/benchmark-runner.md`

**Expertise:** Designing and running rigorous, reproducible benchmarks (timeit, JMH, BenchmarkDotNet, criterion, etc.), fair A/B comparison methodology, honest statistical reporting.

#### 🧪 Test Runner
**File:** `code-review-agents/test-runner.md`

**Expertise:** Writing and reviewing unit/integration test suites across languages (pytest, Jest/Vitest, JUnit, Pester, RSpec, Go `testing`, .NET) — structure, mocking, assertions, code coverage, and detecting tests that provide false confidence.

#### 🔥 Stress Tester
**File:** `code-review-agents/stress-tester.md`

**Expertise:** Load/stress/soak/breakpoint testing design (`k6`, `locust`, `pgbench`, etc.), failure-mode analysis, and safe/authorized testing practices.

---

## 🤖 Using These as Claude Code Subagents

1. Copy the desired `.md` file(s) into `.claude/agents/` in your project (shared with your team via git) or `~/.claude/agents/` (available to you across all projects).
2. Claude Code will auto-invoke the matching agent when your request matches its `description` (e.g., editing an auth handler triggers `security-reviewer`), or you can call one explicitly: "use the performance-reviewer agent on this file."
3. Run `/agents` in Claude Code to see all available agents and their tool scopes.

Each agent's `tools:` frontmatter is scoped to what it actually needs — the two `-reviewer` agents are read-only (`Read`, `Grep`, `Glob`), while `benchmark-runner`, `test-runner`, and `stress-tester` also get `Bash`/`Write` since they execute code.

---

## 🚀 Quick Start

### Using a Domain Architect

1. **Choose the appropriate architect** for your domain
2. **Copy the system prompt** from the corresponding `.md` file
3. **Paste into your AI assistant** (ChatGPT, Claude, etc.)
4. **Start asking questions** or requesting code

### Example Usage

**For GitLab CI/CD:**
```
1. Open: domain-architects/gitlab-architect.md
2. Copy entire content
3. Paste as system prompt in your AI tool
4. Ask: "Design a multi-environment deployment pipeline with security scanning"
```

---

## 🎯 Key Features Across All Architects

### Zero Hallucination Policy
- ✅ Never invent features, APIs, or syntax
- ✅ Explicitly state uncertainty
- ✅ Use web search tools when needed
- ✅ Cite official documentation

### Version Awareness
- ✅ Default to latest stable versions
- ✅ Specify version compatibility
- ✅ Warn about deprecated features
- ✅ Provide migration paths

### Security First
- ✅ No hardcoded credentials
- ✅ Secure coding practices
- ✅ Compliance frameworks
- ✅ Vulnerability prevention

### Production Ready
- ✅ Complete, tested code examples
- ✅ Comprehensive error handling
- ✅ Performance optimization
- ✅ Operational guidance

---

## 📊 Maturity Levels

| Architect | Version | Status | Production Ready |
|-----------|---------|--------|------------------|
| **GitLab** | 2.0.0 | ✅ Stable | Yes |
| **Python** | 2.0.0 | ✅ Stable | Yes |
| **PowerShell** | 2.0.0 | ✅ Stable | Yes |
| **PingIdentity** | 1.0.0 | ✅ Stable | Yes |
| **Java** | 1.0.0 | 🔄 Active Development | Partial |
| **SailPoint** | 1.0.0 | 🔄 Active Development | Partial |
| **RadiantLogic** | 1.0.0 | 🔄 Active Development | Partial |

---

## 📝 License

**MIT License**

Copyright (c) 2025 Agent Architecture Contributors

---

**Excellence is not an option—it's the standard.** 🚀

---

*Last Updated: 2025*  
*Repository Version: 1.0.0*
