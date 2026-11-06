---
name: lean-code
description: "Write the least code that fully solves the task. Reuse existing helpers, the standard library and platform features before adding code or dependencies; no speculative abstractions, options or unrequested features. Use when writing, editing or refactoring code, or when the user asks for lean, minimal, simple or less code."
---

Solve the task with the smallest correct change. Less code means less to read, review, test and break.

## Before writing

1. Restate the exact requirement. Anything outside it is out of scope.
2. Search the codebase for an existing helper, component, hook, util or pattern that already does it, or nearly does. Extend or call it instead of writing a new one.
3. Check the language standard library and platform (browser APIs, framework built-ins, CSS) before writing custom logic.
4. Check already-installed dependencies before adding a new one. Add a dependency only when it replaces substantial, tricky code.

## While writing

- Touch the fewest files and lines needed. Do not reformat, rename or reorganise unrelated code.
- Inline single-use logic. Do not extract a function, type, constant or file until a second caller exists.
- No speculative parameters, config options, flags, generics or extension points.
- No unrequested features, fallbacks or error handling for cases that cannot happen. Validate only at real boundaries (user input, network, external data).
- Prefer data and declarative constructs over branching code.
- Delete code made dead by the change.
- Add no new comments or docs unless asked. Match the surrounding code's existing comment density.
- Match the surrounding code's naming and idioms.

## Before finishing

Review the diff and ask of every added line: can it be removed or replaced by something that already exists without breaking the requirement? If yes, remove it.

## Reporting

In chat, show only the changed lines with minimal context, not whole files.

## Not lean

Lean never means skipping correctness, security checks the task needs, required tests, or accessibility. Never golf code into something unreadable; shorter only counts when it is also clearer.
