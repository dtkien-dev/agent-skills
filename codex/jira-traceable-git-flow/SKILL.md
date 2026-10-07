---
name: jira-traceable-git-flow
description: Prepare, inspect, or safely revert Jira-traceable Git changes while preserving the repository's established branch, commit, and pull- or merge-request flow. Use for ticket-linked branches, commits, pull requests, merge requests, and reviewable reverts; use a more specific repository workflow when one exists.
---

# Jira-Traceable Git Flow

Use the target repository's instructions and accepted history as the source of
truth. Resolve the ticket, repository, remote, source branch, target branch,
and intended operation before mutating Git. Never invent a ticket key or
branch convention. When a repository-specific delivery skill applies, use it instead.

## Branch and commit conventions

Inspect repository guidance and recent accepted branches before proposing a
name. Preserve the verified ticket key in the branch, commit subjects, and
pull or merge request title only when repository convention requires it.
Select the actual target branch from repository or hosting evidence; do not
assume `main`, a release branch, or an environment branch.

An observed convention supports a proposal; it does not authorize creating a
branch, committing, pushing, or opening a pull or merge request. Use
`$interact-with-jira` to verify ticket context and
`$interact-with-git-platform` for hosting operations when those actions are
within the user's request.

Read [Commit convention](references/commit-convention.md) before creating a
commit.

## Safe reverts

Before proposing a revert, inspect the target commit or merged change, its
parents and base, affected files, later dependent commits, current branches,
checks, and whether a revert already exists. Explain the user-visible and
technical effects of reversing it.

Prefer a new ticket-traceable revert branch for a change already merged into
shared history unless repository evidence establishes another safe
convention. Use `git revert` for an additive, reviewable reversal; do not
reset, force-push, or rewrite shared history. For a merge commit, identify the
correct mainline parent from history rather than guessing.

Before a Git mutation, present the exact target, verified base, proposed
branch, expected diff, required checks, push remote and branch, and pull or
merge request target. Execute only actions already authorized by the user.
Stop on conflicts, unresolved dependencies, missing target context, or
uncertain remote results; do not choose a semantic conflict resolution or
repeat a possibly completed mutation automatically.
