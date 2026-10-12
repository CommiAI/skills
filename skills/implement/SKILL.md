---
name: implement
description: Carry a task from supplied context through scoped implementation, review, and verified behavior.
disable-model-invocation: true
---

# Implement

Own the path from the requested outcome to a working result. Determine the execution details from the supplied context and the repository, and judge progress by observable behavior.

## 1. Understand the task

Read the supplied context and repository instructions. Trace the affected behavior through its callers, implementation, and tests. Establish what already works, what must change, and which constraints remain binding.

Translate the intended outcome into checkable completion conditions. Resolve questions through investigation where possible; ask about consequential ambiguities with a recommendation. Surface conflicts that require changing the requested outcome or established design before proceeding with that change.

Proceed when you can explain the affected behavior, its ownership, and how success will be checked.

## 2. Shape and sequence the work

Start from realistic usage. Choose the data structures, interfaces, invariants, and state ownership needed to support it, respecting established design decisions. Prefer clear, local code; introduce an abstraction when it concentrates meaningful responsibility or removes repeated coordination.

Order the work into small increments with an executable check for each. Resolve prerequisites and consequential unknowns early. Choose the smallest coherent change, accounting for every affected consumer and necessary compatibility constraint.

## 3. Coordinate implementation

Implement directly or delegate bounded work where useful. Give each worker the relevant context, owned scope, interface contracts, success conditions, and expected checks.

Parallelize independent work. Keep coupled changes under coordinated ownership, settle shared contracts before splitting implementation, and isolate mutable targets where possible. Serialize access when a shared write target is genuinely required.

Own the integrated result: inspect delegated changes and their evidence before accepting them.

## 4. Build in verified increments

Establish the relevant baseline before changing behavior. For bugs, reproduce the failure through the affected user or consumer path before fixing it.

Implement one meaningful behavior at a time. Where a regression or behavior test provides useful evidence, run it first to establish the intended failure, then implement enough to satisfy it. Assert observable results with independent expected values, exercising real internal logic and substituting dependencies at genuine system boundaries when needed.

Run focused tests and relevant lint, type, or build checks throughout implementation. Keep existing regression coverage meaningful. Complete each increment with its check before beginning dependent work.

Keep edits focused on the intended outcome. Update affected callers together, preserve required compatibility, and remove superseded internal paths once their consumers have migrated. Repeated casts, special cases, or caller workarounds warrant revisiting the approach rather than accumulating patches.

## 5. Review and verify

Review the complete change against the requested behavior, repository standards, interface and state ownership, failure handling, and unintended scope. Fix actionable findings and rerun affected checks, including the relevant broader regression checks on the integrated result.

Use the project's verification skill to verify the affected changes.

Compare the observed result with the completion conditions. Passing static checks, worker reports, or inconclusive results do not establish that the intended behavior works.

## 6. Report the outcome

Summarize what changed and the checks that establish its behavior. Identify unmet conditions, unavailable verification, and remaining risks. Distinguish verified results from assumptions; label the outcome incomplete when required behavior or its proof remains blocked.
