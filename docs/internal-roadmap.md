# Internal Roadmap

This is **this repo's own backlog** — work on maintaining and growing the agent
library itself. It is not part of the template payload: if you created your
project from this repo via "Use this template," this file is about *our*
plans for the agent library, not yours, and you should delete it (root
[`ROADMAP.md`](../ROADMAP.md) is the clean stub meant for your project instead).

**Status legend:** `In Progress` (actively being worked, has an open branch/PR) ·
`Planned` (agreed, not started) · `Idea` (worth doing, not yet agreed/scoped).

Once something here ships, it moves out of this file and into
[`CHANGELOG.md`](../CHANGELOG.md) — same rule as the public roadmap.

---

## Planned

### Template readiness
| Item | Notes |
|---|---|
| ~~Fix `.gitignore`~~ | Done — replaced with real cross-language ignore patterns |
| ~~Note in `CLAUDE.md` that "What this repo is" needs rewriting post-template~~ | Done |
| ~~"After you use this template" section in README~~ | Done |
| Trim-agents guidance | Help a new project figure out which of the 15 agents are actually relevant to them vs. noise (e.g. a pure-Python service doesn't need 5 identity architects) |

### Agent library
| Item | Notes |
|---|---|
| Write `il5-security-baseline.md` | Currently an empty placeholder in `agent-architecture/shared-standards/`; `security-reviewer.md` already claims alignment with it. Scope narrowly to IL5-specific compliance requirements (FIPS-validated crypto, STIG alignment, audit retention) — don't re-litigate what `coding-style-guide.md` or `security-reviewer.md`'s OWASP checklist already own |
| Write `mermaid-patterns.md` | Currently an empty placeholder in `agent-architecture/shared-standards/` |
| Add `terraform-architect` | Coverage gap — no IaC domain architect yet |
| Add `kubernetes-architect` | Coverage gap |
| Add `azure-architect` | Coverage gap |
| Add `aws-architect` | Coverage gap |
| Expand `java-architect` to production-ready | Currently marked partial |
| Expand `sailpoint-architect` with detailed examples | Currently marked partial |
| Expand `radianlogic-architect` with integration patterns | Currently marked partial |

### Quality & CI
| Item | Notes |
|---|---|
| Validate code examples in agent files actually run | No automated check today |
| Markdown lint on every agent file | No automated check today |
| CI pipeline to run both on PR | Depends on the two items above |
| Version compatibility matrix across agents | Cross-reference which agent versions were validated together |

### Repo operations
| Item | Notes |
|---|---|
| Re-check collaborator / branch-protection settings | Repo went public recently; worth confirming `main` is protected as expected |
| Validate the template flow end-to-end | Spin up one real project from "Use this template," confirm all 15 agents auto-load and the new README section actually makes sense from a fresh clone |

## Ideas (not yet scoped)

- Diagram/blueprint-style visualization of the agent architecture (raised in conversation, not committed to)
- Additional review specialists beyond the current 5 (e.g. accessibility reviewer, documentation-quality reviewer)

---

## Keeping this file honest

Same rule as the public roadmap: update this file in the same PR that starts,
finishes, or re-scopes an item. Don't let a completed item linger here once
its branch has merged — move it to `CHANGELOG.md`.
