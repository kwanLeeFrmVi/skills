> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# scan install

> Add various scanning tools seamlessly into your development lifecycle

```bash theme={"dark"}
infisical scan install --pre-commit-hook
```

## Description

The command `infisical scan install` is designed to incorporate various scanning tools seamlessly into your development lifecycle.
Initially, we're offering users the ability to install a pre-commit hook. This hook conducts an automatic scan for any exposed secrets in your commits before they're pushed.

### Flags

<Accordion title="--pre-commit-hook">
  ```bash theme={"dark"}
  infisical scan install --pre-commit-hook
  ```

  **Description**
  Installs a git pre-commit hook that triggers Infisical to scan your staged changes for any exposed secrets prior to pushing.
</Accordion>
