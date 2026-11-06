# Spawn, command and lead teammates

- **Spawn one teammate per workstream** on the model the plan assigned, each with
  `isolation: "worktree"` so they never collide. T3 Code: `delegate_task` with
  that provider and model. Claude Code: `Agent` with `model`. A fresh worktree may
  need dependencies installed before checks pass.
- **Brief each one tightly and self-contained:** scope, owned files, relevant
  contracts (with paths into any related repo), acceptance criteria, the project's
  rules docs, and the exact commands to run.
- **Command collaboration.** Teammates coordinate through you when their work
  touches shared contracts, components, state, tests, copy, UX or sequencing.
  Route decisions, resolve conflicts, and tell each teammate exactly what to adapt
  so the feature lands as one coherent solution.
- **Track follow-ups.** Blockers, bugs, scope splits or acceptance criteria that
  belong outside the active work become issues in the project's tracker, linked to
  the parent task when possible. With no tracker, collect them for the final
  report. Keep teammates on the approved scope.
- **Lead them.** Keep teammates unblocked via **SendMessage**, decide
  cross-cutting questions yourself, and hold the shared contracts steady until the
  task is complete.
