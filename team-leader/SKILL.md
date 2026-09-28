---
name: team-leader
description: Lead delivery of a software task by clarifying requirements with grilling, saving a PRD in Linear, coordinating parallel subagents, and opening a pull request linked to Linear. Use when the user asks for a team lead, agent team, or parallel teammates to take a feature or fix from requirements to PR. Does not apply to ordinary single-agent edits or merely discussing team workflows.
---

# Team Leader

Own the result from a shared understanding to a verified, linked PR. Delegate
bounded work to real subagents; keep scope, coordination, integration, and delivery
with the lead. Reading, installing, or editing this skill does not start a delivery
run or authorize live Linear or GitHub changes.

## 1. Clarify through grilling

Before implementation, locate and read the installed `$grilling` skill. Use the
current skill catalog; on this installation it is at
`/Users/kwan/.agents/skills/grilling/SKILL.md`. If that path has moved, discover the
installed skill instead of copying an old version. If it is unavailable, report
the dependency and pause the interview; do not silently substitute another process.

Apply its decision-tree interview in rounds. Ask decisions whose prerequisites
are settled, include recommendations, and wait for answers before asking dependent
questions. Delegate bounded, read-only fact finding while the lead interviews:
inspect repository instructions, relevant code, available integrations, and any
existing Linear issue or PRD. Do not ask the user to supply discoverable facts.

Resolve the outcome, affected users, scope and exclusions, observable acceptance
criteria, important constraints, and any material product tradeoffs. Reuse decisions
already settled in the conversation. Routine implementation choices belong to the
team unless they change agreed behavior or scope.

Prepare a concrete PRD draft using [Linear delivery](references/linear-delivery.md).
Present it when the decision frontier is empty and obtain the shared-understanding
confirmation required by `$grilling`. When asking, link the actual grilling
`SKILL.md` and quote its requirement: “Do not act on it until the user confirms you
have reached a shared understanding.” Existing confirmation of this same scope
satisfies the gate; do not ask again. Until then, do read-only discovery and drafting,
not implementation or external writes. Respect an explicit user override.

## 2. Save the agreed PRD in Linear

Use the available Linear integration and the procedure in
[Linear delivery](references/linear-delivery.md). Reuse the relevant issue/document
when it exists. Save the full agreed PRD, retrieve it to verify persistence, and
record the real issue identifier and PRD URL before assigning implementation.

Resolve the target team/project from the user's context or existing issue. Ask
only if the destination remains ambiguous after discovery. If Linear is unavailable,
preserve the draft locally and explain what access is missing. Do not claim it was
saved or silently continue past this prerequisite. A user can explicitly choose
to proceed without Linear.

An instruction to carry out this end-to-end workflow covers its task-specific
Linear artifacts and PR creation. Automatic skill selection alone does not expand
authorization: honor requests limited to planning, local work, or a dry run. After
the requirements gate, do not invent additional approval checkpoints for work
already authorized. Merging and deploying are separate actions.

## 3. Organize and run parallel work

Read [Parallel execution](references/parallel-execution.md) before assigning work.
Inspect the actual checkout and repository rules, establish a safe delivery branch,
and decompose the PRD into independently verifiable tasks with dependencies and
exclusive ownership. Follow the repository's branch, package-manager, design, and
validation conventions rather than embedding one project's rules here.

Use the current runtime's subagent tools. This workflow explicitly calls for
parallel subagents: launch at least two useful, independent tasks when the work and
available capacity support that. Do not force simultaneous edits to coupled code;
settle a shared interface first or pair an implementer with independent investigation
or verification work. Explain when no useful parallel split exists. If subagent
tools are unavailable, report that limitation rather than pretending role names
are a team or silently substituting user-owned Codex tasks.

The lead owns the task board and critical path. Keep working on unassigned
integration or coordination while teammates run; do not duplicate delegated work.
Resolve dependencies, relay contract changes, and verify handoffs before accepting
completion. Keep the user informed of meaningful progress and blockers.

If new evidence changes agreed requirements, pause only affected tasks, return
those decisions to the grilling frontier, and update the confirmed PRD before
resuming affected implementation. Continue independent work within settled scope.

## 4. Integrate and quality control

Inspect each teammate's artifacts and combine the work into the delivery branch.
Check the integrated behavior against every acceptance criterion and run the
repository's required checks plus validation appropriate to the change. Individual
agent test results do not prove that the integrated result works.

At the end of team implementation, the lead must perform a final quality-control
pass on the combined result. Review the complete diff and user-facing behavior,
trace each PRD acceptance criterion to evidence, and check seams between teammates'
work. Check for regressions, unfinished paths, and departures from repository
standards. The lead may assign a focused QA pass to a separate agent, especially
for substantive parallel changes; choose someone who did not author the area being
reviewed. Give that agent the agreed criteria and integrated artifacts. The lead
still evaluates the findings, fixes material issues, and reruns affected checks.
Keep the pass proportional to the change.

Do not equate an agent's final message or idle status with completion. The lead
closes the quality-control gate only when the integrated result has inspectable
evidence for the acceptance criteria and material findings are resolved. Record
unverified behavior, environmental blockers, and remaining work accurately.

## 5. Open and cross-link the PR

Follow [Linear delivery](references/linear-delivery.md) to create or update the PR,
link it to the issue and PRD, and save the PR URL back in Linear. Verify both sides.
Report local check results separately from remote CI. Where checks or final quality
control are pending or blocked, keep the PR in draft and state what remains; do not
report finished delivery with unmet acceptance criteria. An open PR is not evidence
of merge or deployment.

Finish with the PR link, Linear issue/PRD links, a short description of the delivered
behavior, validation results, and any concrete remaining blocker. For interrupted
runs, preserve the issue/PRD IDs, branch, task ownership, verified work, and next
action in the existing task record; reconcile actual state before resuming.

## Reference basis

The [Claude Code agent-teams guide](https://code.claude.com/docs/en/agent-teams)
informs bounded assignments, communication, and conflict avoidance. The
[GitHub orchestration skill](https://github.com/github/awesome-copilot/blob/main/skills/ai-team-orchestration/SKILL.md)
informs lead/developer/reviewer responsibilities and durable handoffs. Their
runtime-specific commands and default merge behavior are not requirements here;
use the tools actually exposed by the current environment.
