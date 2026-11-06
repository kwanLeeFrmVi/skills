# Review, integrate and QA

An agent's final message or idle status is not completion. Its own test run
doesn't prove the integrated result works.

## Review every teammate's diff (quality gate)

Don't trust a summary. **Review the actual diff** in its worktree
(`git -C <worktree> diff`) and check that it:

- Meets its ACs and matches the agreed contracts.
- Follows the project's documented rules and reuses existing code instead of
  duplicating it.
- Has no stubs, dead code or scope creep, and passes the project's lint,
  typecheck and tests.

If it falls short, send specific feedback and have the teammate revise in its
worktree. **Iterate until it passes**, then integrate. You are the last line of
defence before merge.

**Escalate on struggle:** if a teammate fails review twice on the same problem,
stop it and hand its workstream and worktree to a teammate one tier heavier.

## Integrate

Bring the worktrees together serially on the delivery branch, following the
project's git workflow. Only you switch branches, commit and run repo-wide
formatting. Run the project's full gates (install, lint, typecheck, test, build —
what CI runs), then verify the feature end to end along the planned flow,
including failure and edge paths.

## Final QA on the combined result

Review the complete integrated diff and user-facing behaviour. Trace every AC to
inspectable evidence, check the seams between teammates' work, and look for
regressions, unfinished paths and departures from repo standards. For substantive
parallel changes, assign a focused QA pass to an agent that authored none of the
area under review; give it the ACs and the integrated artifacts. You still judge
its findings, fix material issues (via the owner or a teammate) and rerun
affected checks. Keep the pass proportional to the change.

Close the gate only when every AC has evidence and material findings are
resolved. Record unverified behaviour, environmental blockers and remaining work
accurately — they go in the PR and the final report.
