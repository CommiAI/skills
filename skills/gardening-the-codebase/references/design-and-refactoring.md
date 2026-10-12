# Design and Refactoring

Use this reference after a candidate is selected, or when implementing an explicitly requested improvement. Shared evaluation principles live in [../SKILL.md](../SKILL.md).

## Caller-first design

Write realistic usage for the common caller before deriving types and module boundaries. Include failures and ordering constraints that callers genuinely face. Describe which domain decisions and invariants the implementation owns, and which facts callers still need to know.

For consequential interface or ownership changes, compare at least two structurally different designs, including a simpler change to the existing shape when viable. Direct comparison is sufficient; parallel agents are optional. Evaluate:

- Capability delivered per unit of interface callers must learn.
- Where knowledge, state changes, and verification concentrate.
- Compatibility and migration burden.
- Whether internal choices leak through the interface.
- New indirection or state introduced to achieve the benefit.

Recommend the strongest design with its tradeoffs. Small, obvious deletions do not require manufactured alternatives. Repeated casts, special-case branches, or caller workarounds during design are evidence to revisit the shape, not automatically proof that it is wrong.

## Dependency and test strategy

A seam is a place where behavior can vary without rewriting the consuming logic; an adapter supplies the dependency there. Keep internal testing seams private when callers do not need them.

| Dependency | Strategy |
|---|---|
| In-process computation or state | Test observable behavior through the module's interface using real logic. |
| Local infrastructure | Prefer an existing realistic local test instance or stand-in; identify fidelity gaps. |
| Remote service owned by the project | Consider an injected transport adapter; combine deterministic logic tests with contract/integration coverage. |
| Third-party service | Isolate the external interaction where useful; use controlled test doubles and verify request/response contracts. |

Production and test adapters can justify a seam, but adapter count alone neither requires nor disproves an abstraction. A test double cannot establish real provider behavior. State what each test catches and misses.

Tests should assert observable outcomes with independent expected values, not restate implementation logic. Preserve useful integration and contract coverage. Replace implementation-coupled tests only after accounting for their meaningful assertions in the new coverage; private helpers are not automatically unworthy of focused tests.

## Migration plan

Before recommending execution, identify:

1. Existing behavior and public compatibility constraints, including errors and side effects.
2. Owned callers, dynamic/configured entry points, and potentially external consumers.
3. Behavior evidence available before restructuring and any coverage gaps.
4. Small ordered changes that reach the target shape while retaining a working system.
5. Obsolete paths and references to remove after their callers migrate.

For fully owned internal interfaces, migrate callers and remove the old path in the same coordinated change when feasible. For external contracts or staged deployments, preserve the necessary compatibility path and define its removal condition. Distinguish intentional compatibility from accidental dual-path architecture.

## Authorized implementation

1. **Pin behavior.** Run the current relevant checks and capture behavior before structural edits. Add characterization tests, a reviewed snapshot, or an old/new equivalence harness where coverage is missing. Record pre-existing failures separately. Lint and type checking supplement, but do not establish, behavioral equivalence. If meaningful behavior cannot be exercised, explain the blocker and agree on limited scope or alternative evidence before proceeding.
2. **Subtract safely.** Remove confirmed unnecessary structure and references, retaining security, trust-boundary, and compatibility requirements. Keep changes inside the chosen improvement.
3. **Reshape incrementally.** Make small changes with the behavior checks green. Track imports, string references, configuration, tests, and documentation for moves and renames. Revisit the design when repeated workarounds expose a missed constraint.
4. **Verify the actual behavior.** Run relevant tests and exercise the affected CLI, UI, service, or library consumer path using the project's existing tools. For published libraries, use a consumer fixture against the built or packed package to check affected exports, supported imports, runtime behavior, and type compatibility where applicable. State which external-consumer assumptions remain unverified. Larger reshapes warrant replayed baselines or old/new output comparisons, including errors and side effects. Report unavailable checks and their consequences rather than claiming equivalence from compilation.
5. **Assess the result.** Explain the concrete reduction in tracing, duplicated rules, caller coordination, or mutable state. Remove speculative additions that did not help, preserving unrelated user work. Summarize the changed structure, held contract, executable evidence, and remaining risks.

Completion requires a justified structural improvement and evidence appropriate to its risk. When verification is blocked, label the outcome incomplete rather than silently weakening the contract.
