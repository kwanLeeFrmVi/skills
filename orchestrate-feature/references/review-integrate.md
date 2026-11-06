# Review, integrate and verify

## Review every teammate's work (quality gate)

Don't trust a teammate's summary. **Review the actual diff** in their worktree
(`git -C <worktree> diff`) and check that it:

- Meets its acceptance criteria and matches the agreed contracts.
- Follows the project's documented rules and reuses existing code instead of
  duplicating it.
- Has no stubs, dead code or scope creep, and passes the project's lint,
  typecheck and tests.

If it falls short, send specific feedback via **SendMessage** and have the
teammate revise in its worktree. **Iterate until it passes**, then integrate. You
are the last line of defence before merge.

**Escalate on struggle:** if a teammate fails review twice on the same problem,
hand its workstream and worktree to a teammate one tier heavier.

## Integrate and verify

Bring the worktrees together on a branch that follows the project's git workflow.
Run the project's full gates (install, lint, typecheck, test, build — what CI
runs), then verify the feature end-to-end along the planned flow, including
failure and edge paths.

Report plainly: what passed, what failed (with output), issues created while
teammates worked, the model that ran each workstream (with any substitutions or
escalations), and anything skipped.
