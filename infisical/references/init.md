> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# infisical init

> Switch between Infisical projects within CLI

```bash theme={"dark"}
infisical init
```

## Description

Link a local project to your Infisical project. Once connected, you can then access the secrets locally from the connected Infisical project.

<Info>
  This command creates a `.infisical.json` file containing your Project ID.
</Info>

The command lists the projects of the organization that your profile uses. To link a project in another organization, change the profile default with `infisical profile set-org`. You can also create a profile for that organization with `infisical profile create`. See [profile](./profile).
