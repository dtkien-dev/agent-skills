---
name: java-service-refactoring
description: Refactor Java service code with evidence-backed flow-impact analysis, repository conventions, and behavior-preservation checks. Use for SOLID, design-pattern, duplication, coupling, transaction-boundary, or maintainability changes; do not apply patterns mechanically.
---

# Java Service Refactoring

Refactor only when a concrete cost exists: duplicated behavior, unstable coupling, an unclear ownership boundary, needless state/indirection, a demonstrated resource cost, or a change-risk caused by the current structure. Follow the repository's conventions before generic SOLID or Refactoring Guru guidance.

## Prove the change boundary

For an unfamiliar flow, establish its behavior from repository documentation, API contracts, source, and focused tests before choosing a refactor. Trace the changed symbol in both directions: inbound callers/controllers/consumers and outbound repositories, clients, caches, events, transactions, and state mutations. Read [Impact analysis](references/impact-analysis.md) before proposing or applying the refactor.

Create a compact impact record with verified evidence:

| Changed symbol | Affected flow | Invariant | Evidence | Coverage needed |
| --- | --- | --- | --- | --- |

Do not claim a flow is unaffected merely because compilation succeeds. Mark untraced callers, reflection/configuration wiring, generated code, and asynchronous consumers as unknown until inspected.

## Choose a refactoring

Read [Principles and patterns](references/principles-and-patterns.md) when considering SOLID or a named refactoring. A principle is a decision aid, not a reason to add an interface, layer, factory, strategy, or class. Preserve public contracts and business state transitions unless the user explicitly asks for behavior change.

Keep a refactor small and independently verifiable. Do not combine it with unrelated formatting, dependency upgrades, generated artifacts, or feature changes. If the safe refactor changes a public API, database schema, transaction boundary, event contract, or authorization path, stop and present the impact rather than treating it as internal cleanup.

## Verify and report

Run focused local tests for the affected flows and repository-required checks. When unit-test classes are excluded from Git by user policy, do not stage them; list local test paths and results separately from the delivery diff.

Report the original cost, refactoring applied, verified affected flows, checks, unverified paths, and residual risk. Use `$code-review` for a defect review and `$simplify` when the goal is broader cleanup rather than a specific Java service refactor.
