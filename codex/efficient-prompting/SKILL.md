---
name: efficient-prompting
description: Turn a goal, ticket, or rough request into a concise, high-signal Codex prompt with explicit scope, evidence requirements, actions, and stopping conditions. Use when the user asks for prompt suggestions, prompt cleanup, or lower-context collaboration.
---

# Efficient Prompting

Write the shortest prompt that lets Codex act safely and produce a reviewable result. Prefer concrete target references over pasting broad repository context.

## Prompt shape

Use only the fields that change the result:

```text
Goal: <outcome>
Scope: <ticket, service, API/path, commit/MR, or files>
Evidence: <authoritative sources to inspect>
Action: <read-only analysis | implement | review | revert>
Constraints: <compatibility, no branch type, no external writes, etc.>
Done when: <specific output/checks>
```

For an unfamiliar business flow, require an Evidence Ledger and state that unverified facts must be labeled `Open question`; do not ask for an implementation proposal in the same prompt unless the evidence phase is complete.

## Reduce context without losing precision

- Name one target ticket/service/API/MR and the exact outcome. Avoid pasting general framework descriptions already discoverable in the repository.
- Give links or paths to the business document and API specification; ask the agent to retrieve the relevant section rather than paste whole documents.
- Separate discovery, implementation, and delivery into successive prompts when each phase may reveal a material decision.
- Name an output limit only when useful, such as “return at most five verified findings.” Do not demand chain-of-thought or repetitive explanations.
- State excluded actions directly: for example, “do not create a branch, push, modify Jira, or run production queries.”

## Delivery guardrails

When the user's workflow excludes unit-test classes from Git, treat test-source paths as an explicit staging exclusion. Run them locally when useful, then list every excluded test path in the delivery proposal. Do not stage, commit, or push them unless the user explicitly reverses that instruction for the exact files.

Before every push, present a final confirmation proposal containing the exact remote, branch, commit SHAs and messages, commit-range diff summary against the verified remote/base, any staged-but-uncommitted diff, checks run, excluded test paths, and commit-convention check. Push only after the user explicitly confirms that exact proposal. Re-run the preflight if the branch, commits, diff, remote, or exclusions change.

## Engineering prompt templates

### Evidence-first discovery

```text
Trace <ticket> in <service> using repository and API evidence.
Read <business document> and <API spec> before source.
Do not propose code or modify files.
Return an Evidence Ledger, verified sequence/table-column map, and Open questions only.
```

### Evidence-backed implementation

```text
Use $surgical-coding for <ticket> in <service>.
Use only the attached/previous Evidence Ledger; inspect missing evidence first.
Implement <bounded behavior>. Preserve <API/compatibility constraint>.
Run <required checks>. Do not create, push, or change a branch.
```

### Commit and push confirmation

```text
Prepare delivery for <ticket/service>.
Do not stage, commit, or push any unit-test class under <test paths>.
Run applicable tests locally and list excluded test files.
Before pushing, show the exact remote, branch, commits, commit-range diff
against the remote base, any staged diff, checks, and excluded files.
Wait for my explicit confirmation to push.
```

### Review

```text
Use $code-review to review <MR/diff/files> for <operation>.
Report only Verified or Likely issues with file:line and a concrete failure path.
Limit to <N> findings. Do not edit code.
```

### Jira-traceable Git preflight

```text
Use $jira-traceable-git-flow to prepare <change or revert> for <ticket>.
Inspect repository instructions, branch topology, and the target commit or PR/MR.
Do not mutate Git or Git hosting.
Return the verified base, proposed branch, expected diff, risks, and checks.
```

