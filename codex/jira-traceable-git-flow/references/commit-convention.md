# Commit convention

Follow the target repository's documented convention first. When it uses
Conventional Commits, use:

```text
<type>(<scope>): <imperative subject>
```

Use the verified ticket key as the scope only when repository policy requires
ticket traceability:

```text
feat(PROJ-123): route international payments
fix(PROJ-456): reject unsupported account categories
```

For a project without ticket-scoped commits, use a meaningful component or
omit the scope according to repository convention:

```text
docs(git-flow): clarify revert preflight
fix: preserve request idempotency
```

Common types:

| Type | Use for |
| --- | --- |
| `feat` | New user-visible capability |
| `fix` | Correction of an observable defect |
| `refactor` | Internal restructuring with preserved behavior |
| `perf` | Measurable performance improvement |
| `docs` | Documentation-only change |
| `build` | Build, dependency, or packaging change |
| `ci` | CI/CD workflow change |
| `chore` | Tooling or maintenance not covered above |
| `revert` | A deliberate reversal of a prior change |

Write an imperative, specific subject without a trailing period. Keep one
coherent, buildable change per commit. Do not mix implementation with
unrelated formatting, generated output, or cleanup. Use a body for material
context, migration or recovery notes, or a non-obvious compatibility
decision; add a breaking-change marker only when an established public
contract actually breaks.

For a revert, prefer the native `git revert` subject and retain its
`This reverts commit <SHA>.` body unless the repository requires a compatible
ticket prefix. Do not create empty commits, fabricate activity, or stage files
the user explicitly excluded.
