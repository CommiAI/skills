---
name: mutation-test
description: Test the strength of a feature's tests with targeted mutations.
disable-model-invocation: true
---

# Mutation Test

Mutation-test the production code changed by the requested feature or fix. Prefer the repository's configured mutation runner and its native test selection; inspect project scripts, configuration, and live `--help` instead of assuming commands. If no runner exists, choose the ecosystem standard and add only the configuration needed for this scope.

## 1. Establish the Scope

Read the repository guidance and inspect the change, its production code, and the tests that exercise it. Target the smallest production-code boundary that represents the changed behavior. Include shared code when the behavior depends on it; use repository-wide mutation only when the user asks for it.

This step is complete when every mutation target maps to behavior in the change and the covering tests are known.

## 2. Prove the Baseline

Run the focused tests for the behavior before mutation testing. Fix relevant failures first. For user-visible behavior, reproduce and verify it through the closest practical end-to-end path.

This step is complete when the mutation target starts from a green, behaviorally representative test baseline.

## 3. Run and Interpret Mutations

Run the configured mutation tool against the scoped production files. Treat each meaningful survivor as a question about observable behavior:

- strengthen a behavioral test when the mutation exposes a missing assertion, boundary, permission, failure, or side effect;
- simplify production code when a survivor reveals behaviorless or redundant code;
- classify an equivalent or unreachable mutant with a concrete reason rather than adding a test that mirrors implementation details.

Rerun the focused tests and mutations after each change. Optimize for meaningful mutants killed, not a perfect score.

This step is complete when every survivor is killed, removed through simplification, or explicitly accounted for.

## 4. Verify and Report

Run the affected package checks and the repository's normal broader verification, including the relevant end-to-end tests. Run the full test suite when practical; otherwise state exactly what remained for CI.

Report the mutation scope, runner, killed and surviving mutants, tests or production code changed, equivalent mutants, and verification commands. Keep generated mutation reports out of version control unless the repository intentionally tracks them.
