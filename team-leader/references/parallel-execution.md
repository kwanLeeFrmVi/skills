# Parallel execution

Read this before delegating implementation. The lead coordinates actual agents,
owns integration, and keeps one authoritative task board.

## Establish ownership

Inspect repository instructions, current branch/base, uncommitted work, and
available agent capacity. Preserve existing user changes. Follow repository branch
conventions; never implement directly on a protected/default branch. Use a separate
checkout when the existing working tree cannot be safely shared.

Choose tasks around independently deliverable outcomes. For each, record:

| Field | Purpose |
| --- | --- |
| Task and PRD criteria | What outcome this task must satisfy |
| Agent and writable paths | Who owns it and where they may edit |
| Inputs and dependencies | What must exist before it can start |
| Contract | Interfaces/data shapes shared with other tasks |
| State and evidence | Ready, active, blocked, awaiting verification, or verified |

Use an existing plan/issue for the board; add Linear sub-issues only when the
workstreams merit separately tracked deliverables. The lead updates the board so
teammates do not race on it. A runtime without atomic task claiming needs explicit
lead assignments. Completion of a prerequisite unlocks dependents only after its
contract and artifacts have been checked.

Assign a shared interface, schema, lockfile, or configuration file to one owner.
Establish its contract before dependent implementation, or serialize that portion.
Ask teammates to propose needed changes outside their paths to the owner.

## Give each teammate a complete brief

Include these details in each assignment, even when conversation context is inherited:

```text
Role and bounded outcome:
Working directory, branch, and applicable repository instructions:
Linear issue/PRD URL and relevant acceptance criteria (include the actual text):
Owned paths and areas that must not be edited:
Dependencies and agreed interfaces:
Expected artifacts and appropriate validation:
Other active owners and how to raise contract changes:
Return changed files, results/evidence, assumptions, blockers, and remaining work.
Report a material ambiguity before implementing affected behavior.
Do not spawn more agents, change branches, commit, push, or mutate Linear/PRs
unless the lead explicitly assigns that responsibility within the user's scope.
```

Include only context needed for the assignment. Inherit the user's model settings
unless there is an explicit reason and authorization to override them. Size the
team to independent work and actual runtime limits, leaving the lead capacity to
coordinate. Do not create dummy roles just to increase the agent count.

## Coordinate the current runtime

In a runtime exposing `collaboration`, use `spawn_agent` for bounded parallel work,
`send_message` for new information, `followup_task` to resume an idle teammate, and
`wait_agent`/`list_agents` to observe progress. Use `interrupt_agent` when an active
assignment must stop. Otherwise use the equivalent tools actually available and
read their schemas. Do not assume another product's team or task tools exist.

Codex sidebar task creation is not a substitute for subagent delegation. Use it
only if the user specifically asks for separate user-owned tasks.

In a shared checkout, all agents see each other's files: only the lead performs
branch switches, commits, and integration-wide formatting. Keep writable paths
disjoint, including generated files. For isolated worktrees, pass an explicit path
and branch, agree how changes return, and let the lead integrate them serially.
Distinct worktrees do not eliminate conflicting edits to the same source file.

Relay changes to all affected owners. Before reassigning a stalled task, stop the
old writer and confirm it is no longer editing, inspect partial work, then transfer
ownership. Never let a replacement race the original agent. Do not repeatedly
retry a failing approach without new evidence; surface a concrete blocker when
progress needs user input or an external change.

Use event notifications or bounded waits instead of rapid polling. While waiting,
do useful unassigned work; when nothing remains independent, wait for the team.
On resumption, reconcile live agents, files, task records, and the actual branch
before issuing new assignments. Do not assume old workers or unfinished patches
vanished.
