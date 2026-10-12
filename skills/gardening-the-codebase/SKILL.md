---
name: gardening-the-codebase
description: Find architectural friction and simplification opportunities, then develop a selected candidate into a concrete, behavior-preserving design.
disable-model-invocation: true
---

# Gardening the Codebase

Improve the codebase by reducing the knowledge required to understand, change, and test it. Start from real friction, subtract unnecessary structure, and concentrate cohesive domain knowledge behind useful interfaces. A healthy design may need no changes.

## Scope and authorization

Discovery and design are read-only by default. A request to audit or explore does not authorize production edits. If the user requests implementation, follow the selected scope and the implementation branch below. Confirm material scope expansion and externally breaking changes before making them. Separate discovered bugs and new features from behavior-preserving refactoring.

## Design principles

- **Depth:** a deep module hides substantial behavior behind a small interface. A module can be a function, class, package, or cohesive subsystem. Its interface includes everything callers must know: inputs, invariants, ordering, errors, configuration, and performance constraints. Depth means leverage for callers, not implementation size or a long call chain.
- **Locality:** concentrate a domain decision, its invariants, and its verification where it is owned. A change should not require rediscovering the same rule across callers.
- **Reader load:** evaluate both layers to trace and mutable state to remember. Ask where a value comes from and what can change it. Prefer explicit ownership, local state, and derived values over synchronized copies.
- **Subtraction:** consider removing obsolete paths, pass-through layers, or duplicated responsibilities before adding an abstraction. Apply the deletion test: if removing a module eliminates complexity, it may be unnecessary; if meaningful complexity spreads into callers, it earns its keep. Preserve wrappers that provide real policy, adaptation, or compatibility.
- **Domain modeling:** make repeated rules and valid state transitions explicit when doing so removes branches, duplicated assumptions, or invalid states. Organize around knowledge and ownership, not merely execution phases. Keep clear, local code when no better model is justified.
- **Boundary discipline:** parse external representations into domain values at trust boundaries; keep framework wiring thin. Remove internal revalidation only when the invariant is demonstrably guaranteed. Account for runtime mutation, untyped inputs, and distinct trust boundaries.
- **Testable contracts:** callers and behavior tests should exercise meaningful interfaces. Internal decomposition can remain private. Choose dependency seams for demonstrated variation or isolation needs, rather than speculative extensibility.

## 1. Ground the scope

Use the subsystem, pain point, or direction the user named. Otherwise inspect available Git history for frequently changed areas, then follow those paths; widen the search if there is no clear hotspot. Without history, use source evidence and ask for direction only if the scope is too broad to investigate usefully.

Read relevant project documentation and existing design rationale, if available. Use established domain terminology and respect known constraints; surface a conflicting proposal only when concrete friction warrants revisiting the decision.

Trace representative caller paths through the affected subsystem and its tests. Establish:

- The behavior callers rely on and the constraints it must preserve.
- Which modules own domain rules, state, external dependencies, and error handling.
- What evidence demonstrates the pain point, including file paths and symbols.

Explore directly or delegate a bounded investigation when available and useful. Grounding is complete when you can explain a representative operation and identify where its rules and state live; a file inventory alone is insufficient.

## 2. Find candidates

Look for friction, not a quota of refactors:

- Understanding one operation requires bouncing across shallow modules or coordinating internal stages.
- Storage, transport, or framework decisions leak into multiple callers.
- State has multiple writers, synchronized copies, or unclear lifecycle ownership.
- Scattered booleans, branches, or repeated assumptions conceal a domain model.
- Public options expose implementation details; internal imports bypass the intended interface.
- Duplicate supported paths or hand-maintained lists drift independently.
- Tests cover isolated helpers while missing the behavior of their coordination, or the existing interface makes important behavior hard to exercise.

For each candidate, compare leaving it unchanged, simplifying the current shape, and introducing new structure. File size, duplication, single callers, and layer counts are investigation signals, not automatic defects. Confirm that apparently dead code is not a dynamic entry point or externally consumed contract.

Keep candidates with a concrete mechanism connecting the current structure to maintenance friction. Distinguish observed evidence from hypotheses, and mark unresolved assumptions.

## 3. Present opportunities

Present concise findings in the conversation, following the user's requested format. Include before/after diagrams when relationships benefit from visualization.

For each candidate include:

- **Evidence:** affected files/symbols and a representative caller or change path.
- **Problem:** the knowledge, coordination, or state tracking imposed on maintainers.
- **Direction:** what responsibility would move, disappear, or become explicit. Describe the shape without prematurely committing to an exact interface.
- **Benefit:** the expected reader-load reduction, locality, caller leverage, and testability improvement.
- **Risk:** compatibility constraints, relevant decisions, and unknowns.
- **Strength:** `Strong`, `Worth exploring`, or `Speculative`, justified by the evidence.

End with the top recommendation and why it beats a smaller change or doing nothing. If no candidate is justified, explain why the examined design should stay. Ask which candidate the user wants to explore; if they already selected one, continue without asking them to choose again.

## 4. Develop the selected design

Read [references/design-and-refactoring.md](references/design-and-refactoring.md) when developing a selected candidate or implementing an authorized change. It contains caller-first design, dependency strategies, migration planning, and verification criteria.

Resolve consequential questions about scope, ownership, compatibility, and observable behavior. Investigate answers available in the repository; ask the user about actual decisions, with a recommendation and its tradeoffs.

Explain the selected design: realistic caller usage, proposed interface and ownership, alternatives where warranted, dependency/test strategy, migration steps, and outstanding decisions. State what complexity disappears and what remains necessary. Scale the explanation to the change; a small cleanup needs only its rationale and verification approach.

Stop at the design explanation unless implementation is requested. For authorized implementation, use the implementation section of the reference and report the changes, verification evidence, reader-load improvement, and any blocked checks.
