---
name: trim-agents
description: Helps a project created from this template decide which of the 16 pre-installed agents to keep vs. delete, based on what the project actually builds. Use when the user says they've just templated this repo and wants to clean up unused agents, or asks which agents they need.
---

# Trim Agents

This template ships all 16 agents active by default (5 code-review specialists + 10 domain architects + 1 content specialist). Most projects only need a fraction of them — a pure-Python service has no use for `sailpoint-architect`, and a project with no PowerShell has no use for `powershell-architect`. Unused agents aren't just clutter: they can still auto-trigger on a request that superficially matches their `description`, producing irrelevant or confusing output.

This skill walks a project through deciding what to keep, in one sitting, rather than leaving it as a someday-task.

## 1. Understand what the project actually is

Don't ask the user to self-report their stack from memory — check first:

- Look for language/framework signals already in the repo: `requirements.txt`/`pyproject.toml` (Python), `pom.xml`/`build.gradle` (Java), `*.ps1`/`*.psm1` (PowerShell), `.gitlab-ci.yml` (GitLab), Ansible `playbooks/`/`roles/` directories, Power BI `.pbix` files, etc.
- If the repo is genuinely empty (a fresh template with no code yet), ask directly: what languages/platforms will this project use, and does it touch identity/IAM (PingIdentity, SailPoint, RadianLogic, ICAM), infra-as-code, or BI/analytics?

## 2. The 5 code-review specialists — default to keeping all of them

`performance-reviewer`, `security-reviewer`, `benchmark-runner`, `test-runner`, and `stress-tester` are language-agnostic — they apply to any codebase, not a specific technology. There's rarely a reason to remove these regardless of stack. Only suggest dropping one if the user explicitly says they don't want that category of review (e.g. "we don't do load testing, drop stress-tester").

## 3. The 10 domain architects — keep only what matches

Go through the catalog in `README.md` and classify each as relevant or not, based on step 1:

| Agent | Keep if the project involves... |
|---|---|
| `python-architect` | Python |
| `java-architect` | Java |
| `powershell-architect` | PowerShell / M365 / Azure automation |
| `ansible-architect` | Ansible / Automation Platform |
| `gitlab-architect` | GitLab CI/CD |
| `powerbi-architect` | Power BI |
| `icam-architect` | Zero Trust / ICAM security architecture |
| `pingidentity-architect` | PingIdentity suite |
| `sailpoint-architect` | SailPoint IGA |
| `radianlogic-architect` | RadianLogic identity platform |

When in doubt, ask rather than guess — deleting an agent is easy to redo (it's one file), but silently keeping something irrelevant defeats the point of this skill.

## 4. `technical-writer` — default to keeping it, same reasoning as the review specialists

Like the code-review specialists, `technical-writer` is language/tech-agnostic — it applies to any project that has documentation, which is nearly all of them. Keep it by default; only drop it if the user explicitly says they don't want an agent involved in writing docs.

## 5. Confirm before deleting anything

This is a destructive, if easily-reversible, action — present the proposed keep/remove list and get explicit confirmation before deleting files. Don't delete on the first pass through the catalog.

## 6. Apply the trim

- `rm .claude/agents/<name>.md` for each agent being dropped.
- Remove the corresponding row from `README.md`'s catalog tables (code review specialists / domain architects / content specialists).
- If the project has started its own `CHANGELOG.md` (see "After you use this template" in `README.md`), note the removal there.

## 7. Leave the door open

Mention that any dropped agent can be brought back later — it's just a file — and that a mid-project pivot (e.g. the project unexpectedly starts using Terraform) is a good reason to re-run this skill or use `add-agent` to bring in something new instead.
