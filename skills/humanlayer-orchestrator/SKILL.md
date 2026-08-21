---
name: humanlayer-orchestrator
description: Orchestrate durable HumanLayer tasks and coding sessions through the HumanLayer CLI.
disable-model-invocation: true
---

# HumanLayer Orchestrator

Act as the user's single liaison. HumanLayer tasks are the durable work record; sessions are execution attempts attached to that record. Keep orchestration state in HumanLayer rather than recreating a parallel tracker in chat or local files.

Use `humanlayer --help` and command-specific `--help` output as the CLI reference.

## 1. Establish Control

1. Run `humanlayer --version` and the relevant `--help` commands.
2. Probe authentication in production with `humanlayer api auth user info` and beta with `humanlayer --beta api auth user info`. Use either authenticated environment and keep every command in the run on that environment. If both work, use the environment containing the relevant task; otherwise prefer production for new work.
3. If neither environment is authenticated, stop HumanLayer mutations and ask the user to run `humanlayer login` or `humanlayer --beta login`.
4. Query online hosts and current tasks before creating anything. Select a host that can access the intended workspace; surface ambiguity instead of guessing across machines.
5. Map each independently shippable change, usually one feature, fix, or PR, to one task. Keep its research, design, implementation, and review sessions in that task. Create another task only for a separately shippable change or a standalone knowledge deliverable.

Control is established when authentication works, an accessible host and workspace are identified, and every shippable change maps to exactly one existing or new task.

## 2. Shape Tasks and Sessions

Decompose the request into independently shippable changes, not phases or arbitrary code layers. A task owns the full path from research through delivery. Use sessions for distinct phases or parallel work within that task, and persist their handoffs as task artifacts.

Use separate worktrees or workspaces for concurrent implementation sessions that can touch the same repository. Serialize only genuine semantic dependencies or shared mutable external state.

For each session prompt, state:

- the outcome and why it matters;
- the exact repository or working directory;
- acceptance criteria and required verification;
- authority boundaries, especially for destructive actions, credentials, merges, and production changes;
- the expected HumanLayer artifact or concise completion report;
- prerequisite task, session, or artifact identifiers.

Tasks and sessions are ready when each task has one shippable outcome and every session has one bounded contribution, a checkable completion criterion, and no unrecorded dependency on another session.

## 3. Dispatch

Create the durable task before launching its sessions. Set the task's workflow type and worktree timing to match the work rather than defaulting every request to implementation. Associate every launched session with its task.

Launch independent sessions concurrently. Launch dependent sessions only after their prerequisite artifact is available, then point the new prompt to that artifact instead of copying a lossy summary into chat.

Prefer the user's explicit coding agent, provider, model, effort, and permissions. Otherwise preserve existing task or session settings. Use the least permissive mode that lets the work proceed; `bypass` requires explicit user authority.

Dispatch is complete when each launched session appears under the intended task and its initial event confirms the full prompt was accepted.

## 4. Reconcile

Treat API state as truth. Reconcile all active tasks in one pass before reporting or launching more work:

1. List sessions for each active task and classify them as working, waiting for input, waiting for approval, completed, interrupted, failed, or lost.
2. Read new events only for sessions whose state changed or whose output is needed for a decision.
3. Send short non-urgent steering to a running session through queued messages.
4. Continue a session that is ready for input. Use `interrupt_and_send` only when its current direction would waste work or violate a changed requirement.
5. Present approvals that change permissions, scope, security posture, cost, production, or irreversible state to the user with evidence and a recommendation. Resolve routine approvals only within authority the user already granted.
6. Persist cross-session deliverables as task artifacts and reference them by task and file name in downstream prompts.

Do not equate process liveness with progress. A session is healthy when its current state and recent events agree on forward movement or a concrete wait.

Reconciliation is complete when every non-terminal session has either a healthy next action, a queued instruction, or a user-visible blocker.

## 5. Recover

Recover from the durable task and session history, not conversation memory.

- **Failed or lost before useful work**: launch a replacement session on the same task with the original contract plus the observed failure.
- **Failed after useful work**: preserve its artifact or working directory, then continue or replace it with explicit recovery instructions.
- **Wrong direction, same outcome**: interrupt and continue the session with the corrected instruction.
- **Alternative direction from a known point**: fork at the relevant user event so both histories remain inspectable.
- **Separately shippable change discovered during work**: create a separate task and link the originating task or artifact in its prompt. Keep new research or implementation needed for the current change in the current task.

Never archive the source task or session until its useful artifacts, decisions, and unfinished changes are accounted for. Recovery is complete when there is one authoritative active attempt for each unfinished deliverable.

## 6. Land the Outcome

Before declaring a task complete:

1. Confirm every required session is terminal or intentionally superseded.
2. Read the final events and required artifacts rather than trusting titles or stale summaries.
3. Verify every acceptance criterion and required test has evidence.
4. Route unresolved review findings or decisions back to the responsible session, or surface them to the user.
5. Archive superseded sessions and completed tasks only when doing so preserves the user's desired history.

Report one consolidated outcome in the user's language: what changed or was learned, verification evidence, links or identifiers for durable artifacts, and only the decisions or blockers that need the user. Keep session mechanics out of the report unless they explain risk or recovery.

The orchestration run is complete only when every requested outcome is delivered, explicitly blocked, or returned as a clearly identified user decision.
