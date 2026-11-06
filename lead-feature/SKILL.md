---
name: lead-feature
description: Lead a feature or fix end to end as team leader — learn the repo, explore in parallel, grill out a PRD, save it in Linear, plan weighted workstreams, spawn and command teammates (each in its own git worktree, on a model sized to its workstream), review every diff, integrate, QA, and open a PR cross-linked to Linear. Use when the user asks to orchestrate a feature, act as team lead, run an agent team or parallel teammates, or take work from requirements to PR. Does not apply to ordinary single-agent edits or merely discussing team workflows.
argument-hint: <issue ID and/or feature/flow description>
---

# Lead Feature

You are the **lead orchestrator and team leader**. Own the result from a shared
understanding to a verified PR linked to Linear. Plan, decompose, delegate,
coordinate, track follow-ups, integrate and QA; teammates implement. Keep scope,
contracts, integration and delivery with you.

Read each linked file only when you reach its step. Reading, installing or
editing this skill does not start a delivery run or authorize live Linear or
GitHub writes.

## Feature spec

$ARGUMENTS

## Authorization

An instruction to run this workflow end to end covers its task-specific Linear
artifacts, branch, commits and PR. Automatic skill selection alone does not:
honor requests limited to planning, local work or a dry run. There are exactly
one approval gate — the **requirements + plan confirmation** in step 3. Don't
invent more. Merging and deploying are separate actions, never in scope
unless the user says so.

## Steps

0. **Learn the project:** [references/learn-project.md](references/learn-project.md).

1. **Explore (read-only, parallel).** Run Explore agents on a light model (Haiku,
   Luna, Sonnet or Terra) to map the code relevant to the spec, looking for code
   to **reuse**, and the contracts the feature depends on or changes (endpoints,
   payloads, events, schemas, migrations, config and env keys, module boundaries)
   in this repo and any related repo. Also look for an existing Linear issue or
   PRD for this work. Keep exploring in the background while you grill — only
   questions that depend on a pending fact wait for it.

2. **Grill out the PRD.** Load the installed `grilling` skill (on this machine
   `/Users/kwan/.agents/skills/grilling/SKILL.md`; if moved, discover it — don't
   copy an old version; if missing, report it and pause). Run its design-tree
   interview in rounds with recommended answers. Where **AskUserQuestion** is
   available and a round is ≤4 discrete choices, use it (recommended option
   first); otherwise use grilling's text format. Cover: outcome and affected
   users, flows, edge cases, contracts, success/failure/empty/loading behaviour,
   copy, rollout (flags, migrations), scope and exclusions, observable acceptance
   criteria. Never ask for discoverable facts. Reuse decisions already settled.
   Routine implementation choices belong to the team unless they change agreed
   behaviour or scope. Draft the PRD per
   [references/linear-delivery.md](references/linear-delivery.md) with stable
   AC IDs (`AC1`, `AC2`, …).

3. **Plan, then confirm once.** When the frontier is empty, write the plan:
   context/why, end-to-end flow, shared contracts (defined up front), behaviour
   per state or event, files to create or modify (reusing what you found), and
   verification. **Decompose into independent parallel workstreams**, one
   teammate each with exclusive file ownership; weight each and assign its model
   per [references/model-tiers.md](references/model-tiers.md). Present the **PRD
   and the plan together** — PRD, then a table of workstream, owned paths, ACs,
   dependencies, weight, model, reason — and ask for the shared-understanding
   confirmation grilling requires, quoting it: “Do not act on it until the user
   confirms you have reached a shared understanding.” The user may change any
   assignment. Call **ExitPlanMode** if in plan mode. Existing confirmation of
   this same scope satisfies the gate. Until confirmed: read-only discovery and
   drafting only — no implementation, no external writes, no spawning.

4. **Save the PRD in Linear** per
   [references/linear-delivery.md](references/linear-delivery.md). Reuse the
   existing issue/document; retrieve it to verify; record the real issue key and
   PRD URL before assigning work. If Linear is unavailable, keep the draft locally,
   say exactly what access is missing, and continue only if the user explicitly
   chooses to proceed without it. A project using another tracker: use that.

5. **Spawn and lead teammates:**
   [references/parallel-execution.md](references/parallel-execution.md).

6. **Review, integrate, QA:**
   [references/review-integrate.md](references/review-integrate.md).

7. **Open and cross-link the PR** per
   [references/linear-delivery.md](references/linear-delivery.md). Keep it draft
   while checks or acceptance verification are pending.

## Finish

Report: PR link; Linear issue and PRD links; the delivered behaviour; each AC
with its evidence; local check results separately from remote CI; the model that
ran each workstream (substitutions, escalations); follow-up issues created; and
anything skipped, unverified or blocked. An open PR is not a merge or a deploy.

For interrupted runs, keep the issue/PRD IDs, branch, task ownership, verified
work and next action in the task record; on resume, reconcile live agents,
worktrees, files and the branch before issuing new assignments.

## Reference basis

The [Claude Code agent-teams guide](https://code.claude.com/docs/en/agent-teams)
and the [GitHub orchestration skill](https://github.com/github/awesome-copilot/blob/main/skills/ai-team-orchestration/SKILL.md)
inform assignments, communication, reviewer roles and handoffs. Their
runtime-specific commands and merge defaults are not requirements; use the tools
the current environment actually exposes.
