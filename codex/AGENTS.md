# Codex Skill Routing

Read [the shared routing guide](../AGENTS.md) first. Use only this agent's format and the invocation specified in each skill.

| Task | Skill |
| --- | --- |
| Bounded implementation or bug fix | `surgical-coding` |
| Defect review of a diff, commit, or PR | `code-review` |
| Security audit or hardening review | `security-review` |
| Split oversized files/functions without changing behavior | `split-code` |
| Java service coupling, SOLID, or pattern refactoring | `java-service-refactoring` |
| Jira-linked branches, commits, PRs, or reverts | `jira-traceable-git-flow` |
| UI design, layouts, and frontend design quality | `anti-ai-design` or `design-taste-frontend`; choose by the requested workflow |
| Flowchart-only compatibility entrypoint | `mermaid-flowchart`; use `technical-diagrams` for other diagram families |
| Improve a prompt | `efficient-prompting` |
| Discover installable skills | `find-skills` |
| Teach step by step and verify understanding | `teach-for-understanding` |
| Windows shell or PowerShell problems | `windows-powershell` |
| Explicit handoff of an accepted record to another Codex CLI session | `handoff-execute` |

## Available skills

- [anti-ai-design](anti-ai-design/SKILL.md)
- [code-review](code-review/SKILL.md)
- [data-debug](data-debug/SKILL.md)
- [design-taste-frontend](design-taste-frontend/SKILL.md)
- [discuss](discuss/SKILL.md)
- [efficient-prompting](efficient-prompting/SKILL.md)
- [execute](execute/SKILL.md)
- [find-skills](find-skills/SKILL.md)
- [handoff-execute](handoff-execute/SKILL.md)
- [interact-with-git-platform](interact-with-git-platform/SKILL.md)
- [interact-with-jira](interact-with-jira/SKILL.md)
- [java-service-refactoring](java-service-refactoring/SKILL.md)
- [jira-traceable-git-flow](jira-traceable-git-flow/SKILL.md)
- [mermaid-flowchart](mermaid-flowchart/SKILL.md)
- [plan](plan/SKILL.md)
- [security-review](security-review/SKILL.md)
- [simplify](simplify/SKILL.md)
- [split-code](split-code/SKILL.md)
- [surgical-coding](surgical-coding/SKILL.md)
- [teach-for-understanding](teach-for-understanding/SKILL.md)
- [technical-diagrams](technical-diagrams/SKILL.md)
- [update-agent-docs](update-agent-docs/SKILL.md)
- [windows-powershell](windows-powershell/SKILL.md)

`global/` contains optional platform instruction templates, not installable skills. Do not apply them as global user policy automatically.
