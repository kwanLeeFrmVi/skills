# Linear PRD and linked PR

Read this while drafting requirements and again at delivery. Use the current
connector schemas; names below describe the capabilities observed in this
installation, not a promise that every runtime exposes identical tools.

## Draft a PRD that can drive delivery

Use the team's existing template when available. Otherwise include the relevant
sections below, scaled to the task:

```markdown
# PRD: <concrete outcome>

## Problem and intended outcome
Who needs this, what fails today, and what changes for them.

## Scope
Included behavior and explicit exclusions.

## Requirements and acceptance criteria
- AC1: An observable result with a clear way to verify it.
- AC2: Relevant error/empty/permission behavior, where applicable.

## Constraints and decisions
Confirmed product choices, relevant repository constraints, and dependencies.
Explicitly distinguish verified facts from user-accepted assumptions.

## Delivery and validation
Workstreams, dependencies, and how acceptance will be demonstrated.

## Open questions
None that block implementation; otherwise return them to grilling.
```

Use stable acceptance-criterion IDs in delegation and verification. Add success
measures, rollout, data/API details, or design references when they affect the
requirements; do not fill sections with invented detail. Avoid duplicating a long
PRD across several artifacts with independent versions.

## Persist before implementation

1. Discover available Linear tools. Retrieve a user-specified issue/document; if
   none was supplied, search for an existing matching task before creating one.
   Resolve team/project from evidence. If multiple destinations remain plausible,
   ask the user to choose. Do not invent IDs, projects, labels, or workflow states.
2. Once the user confirms shared understanding, use the existing task issue or
   create a delivery issue in the resolved team. Preserve unrelated content and
   metadata. Do not create a new project merely to hold a PRD.
3. Prefer a Linear document attached to that issue or its established project,
   following the user's or team's convention. The available `linear_save_document`
   capability supports Markdown content; creation requires a title and one parent.
   Update by the existing document ID on resumed runs. If documents are unsupported,
   the complete PRD in the issue description is an acceptable Linear PRD.
4. Store the document URL in the delivery issue and the issue link in the document
   as needed for navigation. Retrieve the saved artifact and check its agreed scope
   and acceptance criteria. Record the actual issue ID/key and returned URLs.

Use structured arguments with real newlines. Patch the relevant section when
possible; otherwise read the latest content and preserve unrelated text. If a write
times out or returns an uncertain result, look for the artifact before retrying.
Do not blindly create duplicates. On permission/authentication failure, preserve the
draft and surface the exact blocked action instead of looping or claiming success.

## Publish the delivery PR

Follow repository Git policy for the base, branch, commits, and required checks.
Use the available GitHub integration or authenticated `gh`. Inspect remotes and
existing PRs for the delivery branch before creating one. The lead owns publishing;
teammates return implementation evidence unless explicitly assigned otherwise.

The PR title should identify the concrete change. Follow the repository PR template
and include:

- The problem and resulting behavior.
- The Linear issue key with its full URL, plus the PRD URL when separate.
- Verification evidence tied to acceptance criteria and any limitations.

Use a normal related-issue link by default. Use closing keywords only when the PR
fully resolves that issue and that matches the intended workflow. A PR covering
one part of a broader parent issue must not auto-close the parent. Do not assume
Linear's GitHub integration is configured just because the issue key is present.

For multiline PR text through `gh`, write the exact description to a temporary
file and pass `--body-file`; use the verified repository base with `--base`.
Inspect remote checks after creating/updating the PR. Fix failures caused by the
change, run the appropriate checks, and report unrelated or unavailable checks
accurately. Leave the PR in draft while required checks or acceptance verification
remain incomplete; make it ready when the requirements and required checks pass.
Do not merge or deploy unless that action is separately in the user's scope.

## Link back and verify

Save the PR URL to the delivery issue through a supported link operation or a
focused delivery section in its description. Preserve existing links. Include a
concise account of delivered criteria, validation, and remaining work; reuse this
section on retries instead of adding duplicate updates. Follow actual team states
when updating status. Do not mark an issue Done solely because a PR is open.

Retrieve the PR and Linear issue to confirm the PR points to the intended
issue/PRD and the issue points to the correct PR. If the second write fails, retain
the real PR URL and report the incomplete link; resume by repairing that link,
not creating another PR. Return verified links and distinguish delivered code,
passing checks, and any remaining review/merge work.
