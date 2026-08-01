# Roadmap

Forward-looking only — what's not shipped yet and where it stands. Once
something ships, it moves out of here and into [`CHANGELOG.md`](./CHANGELOG.md);
it doesn't live in both.

**Status legend:** `Done` (shipped, listed here briefly for context — full detail
in CHANGELOG) · `In Progress` (actively being worked, has an open branch/PR) ·
`Planned` (agreed, not started) · `Idea` (worth doing, not yet agreed/scoped).

---

## Planned

### Agent library
| Item | Notes |
|---|---|
| Write `il5-security-baseline.md` | Currently an empty placeholder in `agent-architecture/shared-standards/` |
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
| Validate the template flow end-to-end | Spin up one real project from "Use this template," confirm all 15 agents auto-load |

## Ideas (not yet scoped)

- Diagram/blueprint-style visualization of the agent architecture (raised in conversation, not committed to)
- Additional review specialists beyond the current 5 (e.g. accessibility reviewer, documentation-quality reviewer)

---

## Keeping this file honest

Update this file in the same PR that changes an item's status — moving it
between sections, or removing it entirely once it lands in `CHANGELOG.md`.
An item sitting in "In Progress" with a stale branch that already merged is
worse than not tracking it at all.
