---
name: write-gherkin
description: Turn a feature request into a temporary Gherkin specification.
disable-model-invocation: true
---

# Write Gherkin

Turn one proposed feature or change into a concise Gherkin specification that a product owner, developer, and tester can read the same way. The specification is a temporary task artifact, not permanent product documentation.

## 1. Understand the Behavior

Read the request and inspect the existing product when available. Identify the actor, desired outcome, starting state, action, visible result, important failure cases, permissions, and prohibited side effects.

Ask one focused question only when a missing product decision would materially change the behavior. Otherwise use the smallest reasonable assumption and make it visible in the scenarios.

This step is complete when the feature has one clear outcome and every material behavior can be stated from the user's point of view.

## 2. Write the Specification

Return one Gherkin `Feature` containing:

- a short feature name;
- an `As a / I want / So that` description when the actor and benefit are known;
- `Background` only for observable setup shared by every scenario;
- one `Rule` per business rule when grouping improves clarity;
- focused `Scenario` entries for the main path, meaningful failures, permissions, and important boundaries;
- `Scenario Outline` with `Examples` only when the same behavior must be checked with several meaningful values.

Write observable behavior. Describe what the user does and what the product shows or changes. Include absent side effects when they matter, such as no duplicate record, no email, or no unauthorized change.

Use concrete examples instead of vague placeholders. Keep one behavior per scenario, use consistent terms, and reuse setup without hiding behavior behind technical steps.

This step is complete when each scenario has a clear starting state, one action, and outcomes that a human can observe and judge.

## 3. Check the Result

Before returning the specification, confirm:

- every scenario supports the feature outcome;
- the main path and material failure paths are covered;
- permissions and boundaries are included when relevant;
- each `Then` is observable and unambiguous;
- scenarios do not name internal classes, functions, database methods, selectors, mocks, or test commands;
- no QA plan, implementation plan, orchestration instructions, or permanent documentation is added.

Write the specification as `<feature-slug>.feature` in the current task directory. Use a short, descriptive kebab-case filename. Do not add it to the product repository or treat it as permanent documentation. If no task directory is available, return only the specification in a `gherkin` code block.
