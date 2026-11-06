# Learn the project

Assume nothing. Before exploring the feature, establish:

- **Rules:** the agent and contributor docs at the repo root and any they link
  (`CLAUDE.md`, `AGENTS.md`, `CONTRIBUTING.md`, `README`, style or design guides).
  Every teammate builds to these.
- **Toolchain:** the package manager and exact install, lint, typecheck, test and
  build commands, from docs, lockfiles, `package.json` scripts, `Makefile`,
  `pyproject.toml` and CI workflows. What CI runs defines "green".
- **Git workflow:** base branch, branch naming, commit and PR conventions.
- **Related repos:** if the spec or docs name a repo this feature depends on (e.g.
  the backend for a frontend), find it locally and treat it as a **read-only**
  source of truth for contracts. Ask if you can't find it. Don't modify it unless
  the spec says to.
- **Issue tracker:** if the spec names a ticket (`ABC-123`, `#123`, a URL), fetch
  it and its comments with the available tracker tool (MCP or CLI) before planning.
