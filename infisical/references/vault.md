> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# infisical vault

> Change the vault type in Infisical

<Tabs>
  <Tab title="View current Vault">
    ```bash theme={"dark"}
    infisical vault 

    # Example output
    Vaults are used to securely store your login details locally. Available vaults:
    - auto (automatically select native vault on system)
    - file (encrypted file vault)

    You are currently using [file] vault to store your login credentials
    ```
  </Tab>

  <Tab title="Switch vault">
    ```bash theme={"dark"}
    infisical vault set <name-of-vault>

    # Example 
    infisical vault set keychain
    ```
  </Tab>
</Tabs>

## Description

To safeguard your login details when using the CLI, Infisical attempts to store them in a system keyring. If a system keyring can't be found on your machine, the data is stored in a config file.

<Warning>
  Changing the vault removes your profiles and their stored credentials. The new
  vault starts empty, so run `infisical login` after the change.
</Warning>
