# agent-skills

A portable skill collection organized by agent, without organization-specific delivery skills, private Jira snapshots, credentials, or Git history. Banking/payment-specific skills and Antigravity ports are excluded from this distribution.

```text
agent-skills/
├── AGENTS.md           Task routing and maintenance rules
├── codex/              23 Codex skills; $<skill>
│   ├── AGENTS.md
│   ├── <skill>/SKILL.md
│   └── global/         Optional platform instruction templates
├── claude/             9 Claude Code skills; /<skill>
│   ├── AGENTS.md
│   └── <skill>/SKILL.md
├── kiro/               10 Kiro / Kiro Crew skills
│   ├── AGENTS.md
│   └── <skill>/SKILL.md
├── docs/               Shared maintenance and workflow guides
└── scripts/            Installation helpers
```

Start with [AGENTS.md](AGENTS.md) to choose a skill. See [the workflow guide](docs/skills-workflow.md) for collaboration examples.

## Sync skills

Run from the repository root. No arguments selects every direct skill under the relevant agent folder; skill-name arguments select a subset. Whole skill directories are copied. Destination-only files are preserved and must be inspected if comparison reports drift.

| Source | Command | Default destination |
| --- | --- | --- |
| `codex/<name>/` | `./scripts/sync-skills.sh [name ...]` | `~/.codex/skills/<name>/` |
| `claude/<name>/` | `./scripts/sync-claude-skill.sh [name ...]` | `~/.claude/skills/<name>/` |
| `kiro/<name>/` | `./scripts/sync-kiro-skill.sh [name ...]` | `~/.kiro/crew/skills/kiro-skill/<name>/` |

Shell helpers require `rsync`. Override the destination with `CODEX_SKILLS_DEST`, `CLAUDE_SKILLS_DEST`, or `KIRO_SKILLS_DEST` to test against an isolated directory. Kiro preserves its existing installation namespace and does not touch `imported/codex`.

For Codex on Windows, use `powershell.exe -ExecutionPolicy Bypass -File .\scripts\sync-skills.ps1` or `pwsh -File .\scripts\sync-skills.ps1 data-debug plan`; this uses `robocopy.exe`.

Syncing a skill can overwrite same-named installed files. It does not uninstall skills omitted from this collection. Read [maintenance instructions](docs/agent/skill-maintenance.md) before updating or reconciling installed copies.
