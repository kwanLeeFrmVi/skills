---
name: infisical
description: Use the Infisical CLI to authenticate, link projects, run processes with injected secrets, and manage or export secrets. Apply when a user asks to work with Infisical from the command line.
---

# Infisical CLI

Use the CLI for the user's requested project, environment, and secret path. This skill contains the common commands so routine work does not require browsing. Check `infisical --version` and the relevant command's `--help` for installed-version details. If the CLI is absent, install with the platform package manager; on macOS, use `brew install infisical/get-cli/infisical`. Pin the CLI version for production installs.

## Establish context

- For an interactive local session, use `infisical login`, then `infisical login status` to inspect authentication. Run `infisical init` in the intended project directory to create `.infisical.json`. Inspect an existing config before replacing it.
- For machine identities, use the authentication method already configured for the environment. The CLI accepts an access token through `INFISICAL_TOKEN`; specify `--projectId` for machine identity secret operations. For EU Cloud or self-hosted instances, set the documented API URL or domain before authenticating.
- Select an explicit `--env=<slug>` and, when applicable, `--path=<folder>` for operations whose target matters. The CLI defaults to `dev` and the root secret path; verify those defaults are appropriate rather than assuming they match the user's intent. Use environment *slugs*.

## Choose the operation

| Need | CLI pattern |
| --- | --- |
| Start an application with secrets | `infisical run --env=dev --path=/app -- <command>` |
| Read selected values | `infisical secrets get KEY --env=dev` |
| Create or update a value | `infisical secrets set KEY=value --env=dev --path=/app` |
| Delete a value | `infisical secrets delete KEY --env=dev --path=/app` |
| Export to a file | `infisical export --env=dev --path=/app --format=dotenv --output-file=./.env` |

Prefer `infisical run -- ...` when the program only needs environment variables. It injects secrets into the child process without creating an export file. Use `--projectId=<id>` where the project cannot be inferred from `.infisical.json`. `--recursive` includes subfolders and widens the secret set; use it only when needed. `--watch` restarts the child when secrets change and is intended for development.

`secrets set` updates an existing key or creates a new one. It also accepts `KEY=@/path/to/file` and `--file=./.env` for imports. Read the current value or metadata and confirm the intended target before replacing or deleting a secret. Avoid putting secret values directly in shell arguments or transcripts when an input file or a user-managed secret channel is available.

`secrets`, `secrets get`, and `export` can reveal plaintext values in terminal output and logs. Do not print, quote, or paste values into chat; report keys, paths, status, or redacted results. Export only when a file is required, place it outside version control, and check file permissions and ignore rules. `--plain --silent` is for scripts that need a value, not for inspection. Never commit an exported secrets file.

For shell loading, `--format=dotenv-eval` quotes values for POSIX shells, but secret **names** are not escaped. Only `eval` or `source` that output when all names are trusted valid shell identifiers. Prefer `infisical run` for ordinary commands.

## Bundled command reference

These are local Markdown copies of Infisical's CLI command pages. Select only the relevant page; there is no need to browse for routine commands. Use the installed CLI's `--help` if behavior differs from a bundled page.

| Task | Local docs |
| --- | --- |
| Install and configure access | [overview](references/overview.md), [login](references/login.md), [logout](references/logout.md), [init](references/init.md), [profile](references/profile.md), [reset](references/reset.md) |
| Inject, read, or write secrets | [run](references/run.md), [secrets](references/secrets.md), [export](references/export.md), [dynamic-secrets](references/dynamic-secrets.md), [agent-proxy](references/agent-proxy.md) |
| Identity and administration | [org](references/org.md), [user](references/user.md), [token](references/token.md), [service-token](references/service-token.md), [bootstrap](references/bootstrap.md) |
| Infrastructure and access | [gateway](references/gateway.md), [relay](references/relay.md), [kmip](references/kmip.md), [vault](references/vault.md), [pam](references/pam.md), [pam-agentic](references/pam-agentic.md), [agent-vault](references/agent-vault.md) |
| Scan for exposed secrets | [scan](references/scan.md), [scan-git-changes](references/scan-git-changes.md), [scan-install](references/scan-install.md) |

Additional CLI guides: [quick usage](references/usage.md), [project config](references/project-config.md), [scanning overview](references/scanning-overview.md), [FAQ](references/faq.md), and [Linux package repository migration](references/cloudsmith-migration.md).
