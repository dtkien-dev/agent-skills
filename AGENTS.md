# Agent Guide

## Choose the agent format first

- Codex: read `codex/<skill>/SKILL.md`; invoke `$<skill>`.
- Claude Code: read `claude/<skill>/SKILL.md`; invoke `/<skill>`.
- Kiro / Kiro Crew: read `kiro/<skill>/SKILL.md`; use the exact frontmatter name and invocation documented there. Folder names may differ from `kiro-` skill names.
- Use only skills available in the current agent's folder. Do not copy another agent's tool names or pretend an absent port is supported. See each folder's `AGENTS.md` for its inventory.
- Load a skill when the user names it or its description matches the actual task. Read the full `SKILL.md`, then only relevant linked resources. Simple unrelated work does not need a skill.

## When to use a skill

| Task | Skill to read in the current agent's folder |
| --- | --- |
| Discuss requirements and record decisions | `discuss` |
| Produce a reviewed implementation plan | `plan` |
| Execute an approved plan or execution-ready discussion tracker | `execute` |
| Simplify changed code while preserving behavior | `simplify` |
| Work with GitHub, GitLab, or Gitea | `interact-with-git-platform` |
| Read or update Jira | `interact-with-jira` |
| Inspect database connectivity, metadata, queries, or plans | `data-debug` |
| Create architecture, workflow, sequence, data-flow, or state diagrams | `technical-diagrams` |
| Create or refresh repository agent documentation | `update-agent-docs` |

For Codex-only implementation, reviews, UI work, teaching, and prompt help, read [codex/AGENTS.md](codex/AGENTS.md). For Kiro's independent Codex CLI review, read [kiro/AGENTS.md](kiro/AGENTS.md).

## Maintain this collection

- Repository skill directories are authoritative. Before adding, changing, validating, or syncing a skill, read [docs/agent/skill-maintenance.md](docs/agent/skill-maintenance.md).
- Keep each complete skill directory together, including scripts, references, schemas, engines, and assets. Preserve agent-specific tools and invocation syntax.
- Keep shared engines aligned across existing ports; do not create missing ports by relabeling Codex instructions.
- Database work is read-only by default and uses the `data-debug` bundled Docker workflow. External writes require authorization under the relevant skill and session.
- Read `discuss`, `plan`, and `execute` together when changing the direct discussion-to-execution contract. An execution-ready discussion tracker is the single record; no duplicate plan is required.
- When changing Jira REST contracts, run that port's `scripts/validate_rest_registry.py` before source/mirror checks.
- Before changing a plugin, read [docs/agent/plugin-maintenance.md](docs/agent/plugin-maintenance.md); install complete plugins rather than flattening nested skills.
- Keep organization-private metadata, credentials, private environment files, and machine-local configuration out of this shared collection. Use placeholders and runtime configuration.
