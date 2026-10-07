# Skills workflow

Choose the format through [AGENTS.md](../AGENTS.md). Examples below use Codex syntax; use the corresponding Claude or Kiro invocation from its skill file.

1. For unclear requirements, use `discuss` to record evidence, decisions, and open questions.
2. Use `plan` when a reviewed implementation plan is requested. Use `execute` for an approved plan or an execution-ready discussion tracker; keep its exact record bundle.
3. For bounded Codex edits, use `surgical-coding`. For Java service design changes, use `java-service-refactoring`; first trace callers, API contracts, transactions, and outbound effects.
4. Use `code-review` for defects, `security-review` for security concerns, `simplify` for cleanup, or `split-code` for structural extraction when available in the agent's folder.
5. Use `interact-with-jira` for Jira and `interact-with-git-platform` for hosting operations. Codex `jira-traceable-git-flow` preserves an evidenced ticket-linked repository convention.
6. Use `technical-diagrams` for technical visuals and `data-debug` for read-only database troubleshooting through its bundled Docker workflow.

A compact request names the target, outcome, evidence, constraints, and completion check:

```text
Use $surgical-coding on <files/symbols>.
Inspect <API contract> and the nearest relevant implementation/tests.
Implement <bounded behavior>, preserving <compatibility constraint>.
Run <focused checks>. Do not commit, push, or change external systems.
```

Skills do not supply missing business rules or authorize unrelated mutations. Read only the references relevant to the current phase and label unresolved evidence explicitly.
