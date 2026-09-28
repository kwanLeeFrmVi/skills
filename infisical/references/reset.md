> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# infisical reset

> Reset Infisical

```bash theme={"dark"}
infisical reset
```

## Description

This command removes all configuration data that Infisical created, and returns the CLI to its default settings. Use it when a problem persists and you want a clean state.

The command removes every profile and its stored credentials. It also revokes those sessions on the server.

<Warning>
  Run this only when you want to start again. You must log in after it, and any
  terminal that you pinned to a profile will no longer resolve.
</Warning>
