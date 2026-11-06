---
name: resolve-pr-review
description: Read and resolve GitHub pull request review comments by checking each claim against the current code and requirements. Use when the user asks to address PR feedback, fix review comments, or clear review threads. Do not use for a general code review with no existing comments.
---

# Resolve PR Review

Treat review comments as hypotheses, not instructions. Resolve the underlying issue when a comment is right; explain with evidence when it is wrong. Own the result across the whole PR, including interactions between comments.

## Establish the review state

Identify the exact PR and repository. Read repository instructions, the PR description and linked requirements, the current diff and head commit, and all relevant review threads with their replies and resolution status. Include comments GitHub marks outdated: the line may have moved while the concern remains. Distinguish review threads from general PR discussion. Use the available GitHub integration or `gh`; if access is missing, state which comments could not be read instead of assuming there are none.

Preserve unrelated local changes. Before editing, confirm the checkout and branch correspond to the PR, and note whether the PR head has advanced since comments were fetched. Reconcile new commits or comments before publishing responses or marking threads resolved.

## Decide on each concern

For each actionable thread, inspect the surrounding implementation and any relevant tests, contracts, history, or documentation. Identify the reviewer's underlying claim separately from their proposed fix. Classify it as valid, partly valid, already addressed, incorrect, or unclear. Seek a minimal reproduction or other concrete evidence when behavior is disputed. A suggestion can be wrong even if its underlying concern is real; solve the concern with the approach that best fits the codebase.

Do not change code merely to satisfy a comment. Check whether the proposed change breaks another requirement, introduces a regression, or rests on an inaccurate premise. If the evidence is inconclusive and the choice would change product behavior or scope, ask for the missing decision; continue with independent threads.

## Resolve and verify

- **Valid or partly valid:** Make the smallest coherent fix, update meaningful tests when needed, and run the repository's required checks plus focused verification. Check the integrated PR after all fixes, since two individually sound suggestions may conflict.
- **Already addressed:** Verify against the current PR head and point to the relevant code or commit.
- **Incorrect:** Keep the correct code. Explain the specific premise that fails and cite the code, requirement, or test that demonstrates it. Be concise and respectful; avoid dismissing the reviewer or claiming certainty beyond the evidence.
- **Unclear:** Ask a focused question in the thread when the answer is needed to finish that concern. Do not guess or silently close it.

When the task includes updating the GitHub PR, publish verified fixes to its branch and reply to each handled thread with what changed or why no change is warranted. Do not merge the PR or dismiss a review unless separately requested.

## Finish by resolving review conversations

At the end of the PR update, reconcile the live PR state: new comments, current head, thread statuses, and CI. Then explicitly mark every settled review conversation (review thread) as resolved using the GitHub integration or `gh`; posting a reply alone does not complete the task. This includes verified fixes published to the PR branch, concerns already addressed at the current head, and incorrect claims answered with evidence when no substantive disagreement remains. Resolve threads only when the repository workflow permits it. Leave substantive disagreements, unanswered questions, and unverified fixes open.

Fetch the thread statuses again to confirm resolution succeeded. If access or tooling prevents resolving a settled thread, report that thread and the blocker instead of claiming it is resolved. Report which concerns were fixed, rejected with reasons, already addressed, or remain open; include validation results. Do not claim complete resolution while a known actionable concern remains.
