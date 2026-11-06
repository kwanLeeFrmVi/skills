# Spawn, command and lead teammates

You coordinate real agents, own integration, and keep one authoritative task
board. If the runtime has no subagent tools, say so — don't pretend role names
are a team.

## Establish the branch and ownership

Inspect repository rules, current branch and base, uncommitted work and agent
capacity. Preserve existing user changes. Create the delivery branch per the
repo's conventions; never implement on a protected/default branch.

Keep the approved plan's table as the board. For each workstream track:

| Field | Purpose |
| --- | --- |
| Workstream and AC IDs | The outcome it must satisfy |
| Teammate, model, worktree, owned paths | Who owns it and where they may edit |
| Inputs and dependencies | What must exist before it starts |
| Contract | Interfaces/data shapes shared with others |
| State and evidence | Ready, active, blocked, awaiting review, or verified |

Only you update the board. Add Linear sub-issues only when a workstream merits a
separately tracked deliverable. A dependency unlocks its dependents only after
you've checked its contract and artifacts.

Give each shared interface, schema, lockfile or config file one owner. Settle the
contract before dependent work starts, or serialize that part. Teammates propose
changes outside their paths to the owner, through you.

Launch at least two useful independent workstreams when the work supports it.
Don't force parallel edits to coupled code — pair an implementer with independent
investigation or verification instead, and say when no useful split exists. Don't
create dummy roles to inflate the count. Leave yourself capacity to coordinate.

## Spawn

One teammate per workstream, on the model the approved plan assigned (the
approval is the authorization to override the inherited model), each in its own
git worktree so they never collide:

- **Claude Code:** `Agent` with `model` and `isolation: "worktree"`; follow up
  with `SendMessage`, stop with `TaskStop`.
- **T3 Code:** `delegate_task` with the provider and model.
- **Codex `collaboration`:** `spawn_agent`, `send_message`, `followup_task`,
  `wait_agent`/`list_agents`, `interrupt_agent`. Sidebar task creation is not
  delegation; use it only if the user asks for user-owned tasks.
- **Elsewhere:** the equivalent tools actually exposed; read their schemas.

A fresh worktree may need dependencies installed before checks pass. Distinct
worktrees don't remove conflicts from editing the same source file — keep owned
paths disjoint, including generated files.

## Brief each teammate completely

Self-contained, even when context is inherited, and only what the job needs:

```text
Role and bounded outcome:
Worktree path, branch, and the repo's rules docs to follow:
Linear issue/PRD URL and the AC IDs it owns (include the actual AC text):
Owned paths, and areas it must not edit:
Dependencies and agreed contracts (with paths into any related repo):
Exact install / lint / typecheck / test commands to run:
Other active owners and how to raise a contract change (through the lead):
Return: changed files, check results/evidence, assumptions, blockers, remaining work.
Report a material ambiguity before implementing the affected behaviour.
Do not spawn agents, change branches, commit, push, or touch Linear/PRs
unless the lead assigns that explicitly.
```

## Command and lead

- **Route collaboration through you.** When work touches shared contracts,
  components, state, tests, copy, UX or sequencing, decide it, then tell every
  affected teammate exactly what to adapt so the feature lands as one solution.
  Hold the contracts steady.
- **Keep teammates unblocked** and on the approved scope. Keep working on
  unassigned integration or coordination meanwhile; never duplicate delegated
  work. Use notifications or bounded waits, not rapid polling.
- **Track follow-ups.** Blockers, bugs, scope splits or ACs that belong outside
  the active work become tracker issues linked to the parent; with no tracker,
  collect them for the final report.
- **Requirements change?** Pause only the affected workstreams, return those
  decisions to the grilling frontier, update the confirmed PRD in Linear, then
  resume. Independent work continues.
- **Reassigning.** Stop the old writer and confirm it has stopped, inspect its
  partial work, then transfer ownership. Never let a replacement race the
  original. Don't retry a failing approach without new evidence; surface a
  concrete blocker instead.
- Keep the user informed of meaningful progress and blockers.
