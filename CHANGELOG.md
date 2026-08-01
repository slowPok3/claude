# Changelog

All notable changes to the Agent Architecture repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Changed

- 🗂️ **Consolidated the repo around `.claude/agents/` as the single source of truth.** Deleted `agent-architecture/code-review-agents/` and `agent-architecture/domain-architects/` — their content was a byte-for-byte duplicate of what's now only in `.claude/agents/`, kept in sync manually since the previous entry below. Removing the second copy removes the drift risk entirely.
- 📄 Moved `agent-architecture/CHANGELOG.md` → `CHANGELOG.md` (repo root).
- 📄 Consolidated `agent-architecture/README.md` and `agent-architecture/CLAUDE.md` into root `README.md` and `CLAUDE.md`. Root README now catalogs every agent plus instructions for using them both with Claude Code and by copy-pasting into other AI tools; root CLAUDE.md carries the orchestration guidance and agent-authoring conventions.
- 📁 `agent-architecture/` now holds only what can't live in `.claude/agents/`: `Principal-Solution-Architect.md` (a cross-platform orchestrator persona, not a functional Claude Code subagent — see below) and `shared-standards/`.
- 🔁 Converted all 10 domain-architect files to Claude Code subagent format (added `name`/`description`/`tools`/`model` YAML frontmatter), matching the code-review-agents conversion below.
- 🔁 Stripped a stray UTF-8 BOM from `powershell-architect.md` that would have broken YAML frontmatter parsing.
- 🚫 `Principal-Solution-Architect.md` was converted to subagent frontmatter but then **kept out of `.claude/agents/`** — a Claude Code subagent cannot invoke other subagents, so its core "decompose → delegate → synthesize" behavior can't actually function as one. The file stays in `agent-architecture/` for its original use case (pasting as a system prompt into tools without native subagent orchestration).
- 📄 Added root `CLAUDE.md`: rewrites the Principal Solution Architect's orchestration guidance, cross-cutting standards (no hallucination/secrets/PII, least privilege, error handling, modern tooling), and domain-architect-vs-review-agent guidance as direct instructions for Claude Code's main session, which is what actually performs multi-agent orchestration in this repo.
- 🔁 Renamed and reformatted all code-review agent files as **Claude Code subagents** (added `name`/`description`/`tools`/`model` YAML frontmatter):
  - `performance-review-agent.md` → `performance-reviewer.md`
  - `security-review-agent.md` → `security-reviewer.md`
  - `benchmark-agent.md` → `benchmark-runner.md`
  - `stress-test-agent.md` → `stress-tester.md`
  - `pester-agent.md` → generalized and renamed to `test-runner.md` (was PowerShell/Pester-only; now framework-agnostic — detects and applies pytest, Jest/Vitest, JUnit, Pester, RSpec, Go `testing`, or .NET conventions per project, with Pester retained as one worked example)
- 📁 `.claude/agents/` now holds all 15 agents (5 code-review + 10 domain architects) for direct use as a Claude Code project template; confirmed no `name:` collisions among them.

### Added

#### Code Review Agents

- 📁 Added 5 narrow, review-focused (not generative) specialist prompts, each usable as a Claude Code subagent

**Performance Reviewer (v1.1.0)**
- ✅ Algorithmic complexity, memory/allocation, I/O, concurrency, and database query review checklists
- ✅ Severity-scaled, cited-finding output format
- ✅ Read-only tool scope (`Read`, `Grep`, `Glob`)

**Security Reviewer (v1.1.0)**
- ✅ OWASP-aligned checklist (injection, auth, access control, data exposure, XXE, XSS/CSRF, SSRF, path traversal, crypto, dependencies)
- ✅ Aligned with `shared-standards/il5-security-baseline.md`
- ✅ Read-only tool scope (`Read`, `Grep`, `Glob`)

**Benchmark Runner (v1.1.0)**
- ✅ Rigorous benchmark design methodology (warm-up, repetitions, variance reporting)
- ✅ Per-language tool guidance (timeit, JMH, BenchmarkDotNet, criterion, `go test -bench`)
- ✅ Execution tool scope (`Bash`, `Write`) to actually run benchmarks

**Test Runner (v1.0.0)**
- ✅ Framework-agnostic test structure, mocking, and assertion conventions (pytest, Jest/Vitest, JUnit, Pester v5, RSpec, Go `testing`, .NET)
- ✅ Checklist for detecting false-confidence tests in existing suites
- ✅ Execution tool scope (`Bash`, `Write`, `Edit`) to run and author test files

**Stress Tester (v1.1.0)**
- ✅ Load/stress/soak/breakpoint testing methodology
- ✅ Explicit authorization/safety constraints against unauthorized DoS
- ✅ Execution tool scope (`Bash`, `Write`) to run load-test scripts

---

## [1.0.0] - 2025-01-15

### Added

#### Repository Structure
- 🎉 Initial repository setup
- 📁 Organized domain-architects directory
- 📁 Created shared-standards directory
- 📝 Comprehensive README.md
- 📋 CHANGELOG.md for version tracking
- 🚫 .gitignore for common exclusions

#### Domain Architects

**GitLab Architect (v2.0.0)**
- ✅ Zero hallucination policy
- ✅ Version awareness (GitLab 15.0+)
- ✅ Active tool usage guidance
- ✅ Comprehensive troubleshooting examples
- ✅ Advanced pipeline patterns
- ✅ Runner configuration best practices
- ✅ Version-specific features guide
- ✅ Deployment model selection framework
- ✅ GitOps tool integration guidance
- ✅ Security and compliance frameworks

**Python Architect (v2.0.0)**
- ✅ Python 3.10+ modern features
- ✅ Strict type hinting requirements
- ✅ Async/await best practices
- ✅ Security hardening guidelines
- ✅ Testing with pytest examples
- ✅ CI/CD integration patterns
- ✅ Performance optimization guide
- ✅ Dependency management (pyproject.toml)

**PowerShell Architect (v2.0.0)**
- ✅ PowerShell 7.0+ focus
- ✅ Strategic module selection (Az, Graph, PnP)
- ✅ Service-to-module mapping (12+ services)
- ✅ Performance benchmarks
- ✅ Runspace vs ForEach-Object -Parallel guidance
- ✅ Security best practices
- ✅ Deprecation warnings

**PingIdentity Architect (v1.0.0)**
- ✅ Full product suite coverage
- ✅ Protocol selection guidance (SAML, OIDC, OAuth)
- ✅ Zero Trust architecture patterns
- ✅ High Availability configurations
- ✅ Security hardening

**Java Architect (v1.0.0)**
- ✅ Initial version
- 🔄 Active development

**SailPoint Architect (v1.0.0)**
- ✅ Initial version
- 🔄 Active development

**RadiantLogic Architect (v1.0.0)**
- ✅ Initial version
- 🔄 Active development

#### Meta-Architect

**Principal Solution Architect (v1.0.0)**
- ✅ Cross-domain orchestration
- ✅ Technology stack selection
- ✅ Integration architecture
- ✅ Trade-off analysis framework

#### Shared Standards
- 📝 Coding style guide (placeholder)
- 🔒 IL5 security baseline (placeholder)
- 📊 Mermaid patterns (placeholder)

---

## [Unreleased]

### Planned

#### Enhancements
- [ ] Complete shared-standards documentation
- [ ] Add Terraform architect
- [ ] Add Kubernetes architect
- [ ] Add Azure architect
- [ ] Add AWS architect
- [ ] Expand Java architect to production-ready
- [ ] Expand SailPoint architect with detailed examples
- [ ] Expand RadiantLogic architect with integration patterns

#### Documentation
- [ ] Add contribution guidelines (CONTRIBUTING.md)
- [ ] Add code of conduct
- [ ] Add issue templates
- [ ] Add pull request templates
- [ ] Add architecture decision records (ADRs)

#### Quality Improvements
- [ ] Add automated testing for code examples
- [ ] Add linting for markdown files
- [ ] Add CI/CD pipeline for validation
- [ ] Add version compatibility matrix

---

## Version History Summary

| Version | Date | Description |
|---------|------|-------------|
| 1.0.0 | 2025-01-15 | Initial release with 7 domain architects |

---

## Notes

### Versioning Strategy

- **Major version (X.0.0)**: Breaking changes, major restructuring
- **Minor version (0.X.0)**: New architects, significant enhancements
- **Patch version (0.0.X)**: Bug fixes, minor improvements

### Individual Architect Versions

Each domain architect maintains its own version number:
- GitLab Architect: v2.0.0
- Python Architect: v2.0.0
- PowerShell Architect: v2.0.0
- PingIdentity Architect: v1.0.0
- Java Architect: v1.0.0
- SailPoint Architect: v1.0.0
- RadiantLogic Architect: v1.0.0

---

*For detailed changes within each architect, see the version information in the respective `.md` files.*
