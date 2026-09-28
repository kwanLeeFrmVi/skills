> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# infisical user

> Manage logged in users

```bash theme={"dark"}
infisical user
```

## Description

This command manages the accounts that are logged in to the CLI.

Each login is stored as a profile: an account on the specified Infisical instance, and the organization you chose for it. See [profile](./profile) to create profiles, to select one per terminal or per directory, and to work in several organizations at the same time.

### Sub-commands

<Accordion title="infisical user switch" defaultOpen="true">
  Pick which profile the CLI uses by default on this machine.

  ```bash theme={"dark"}
  infisical user switch
  ```

  <Tip>
    `infisical profile use <name>` does the same thing without a prompt.
    `infisical profile list` shows the available profile names.
  </Tip>
</Accordion>

<Accordion title="infisical user update domain">
  Change the Infisical instance that a profile points to. Use this to move a profile between Infisical Cloud and your own self-hosted instance.

  ```bash theme={"dark"}
  infisical user update domain
  ```

  <Warning>
    The command clears the stored session of that profile. Run
    `infisical login --profile <name>` to sign in to the new instance.
  </Warning>
</Accordion>

<Accordion title="infisical user get token">
  Use this command to get your current Infisical access token and session information. This command requires you to be logged in.

  The command will display:

  * Your session ID
  * Your full JWT access token

  ```bash theme={"dark"}
  infisical user get token
  ```

  Example output:

  ```bash theme={"dark"}
  Session ID: abc123-xyz-456
  Token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
  ```

  ### Flags

  <Accordion title="--plain">
    Output only the JWT token without formatting (no session ID)

    Default value: `false`

    ```bash theme={"dark"}
    # Example
    infisical user get token --plain
    ```

    Example output:

    ```bash theme={"dark"}
    eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
    ```
  </Accordion>
</Accordion>
