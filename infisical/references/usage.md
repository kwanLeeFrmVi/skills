> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Quickstart

> Manage secrets with Infisical CLI

The CLI is designed for a variety of secret management applications ranging from local development to CI/CD and production scenarios.

<Tabs>
  <Tab title="Local development">
    The steps below authenticate the CLI with your own account, link a codebase to an Infisical project, and inject the secrets you have access to into your local development process as environment variables.

    <Note>
      If you prefer to learn by watching, follow along with our [step-by-step video tutorial](https://www.youtube.com/watch?v=zYCeELjcgQ4).
    </Note>

    ## Step 1: Log in to Infisical

    Authenticate the CLI with your Infisical account.

    ```bash theme={"dark"}
    infisical login
    ```

    The prompt asks which instance you want to use. Select **Infisical Cloud (US)**, **Infisical Cloud (EU)**, or **Self-hosted**, then finish signing in through your browser.

    <Note>
      On a machine with no browser, such as a remote SSH session, WSL 2, or Codespaces, run `infisical login -i` to log in from the terminal instead.
    </Note>

    ## Step 2: Link your codebase to your project

    Go to the directory of the codebase you're working on and link it to your Infisical project.

    ```bash theme={"dark"}
    cd /path/to/your/project
    infisical init
    ```

    Select your organization and project when prompted. This creates an `.infisical.json` file with your [local project settings](/docs/cli/project-config), so the commands you run next don't need a project ID.

    <Note>
      `.infisical.json` holds no secret values, so you can safely commit it to version control. Everyone who clones the repository is then pointed at the same project.
    </Note>

    ## Step 3: Start your application with secrets injected

    Run your usual start command through `infisical run`, placing it after the `--` separator.

    <CodeGroup>
      ```bash Node.js theme={"dark"}
      infisical run --env=dev -- npm run dev
      ```

      ```bash Python theme={"dark"}
      infisical run --env=dev -- flask run
      ```

      ```bash Go theme={"dark"}
      infisical run --env=dev -- go run main.go
      ```

      ```bash Ruby theme={"dark"}
      infisical run --env=dev -- bundle exec rails server
      ```

      ```bash Java theme={"dark"}
      infisical run --env=dev -- ./mvnw spring-boot:run
      ```

      ```bash .NET theme={"dark"}
      infisical run --env=dev -- dotnet run
      ```
    </CodeGroup>

    The CLI fetches the secrets you have access to and passes them to your application as environment variables. Your application reads them the same way it always has, through `process.env` in Node.js or `os.environ` in Python, so you don't need to change any application code.

    <Note>
      By default, `infisical run` only injects the secrets sitting at the root of the environment, so anything inside a folder is skipped. If your secrets live in [folders](/docs/documentation/platform/folder), you can specify a folder to include using `--path`:

      ```bash theme={"dark"}
      infisical run --env=dev --path="/backend" -- npm run dev
      ```

      If you also need the secrets in that folder's subfolders, add `--recursive`:

      ```bash theme={"dark"}
      infisical run --env=dev --path="/backend" --recursive -- npm run dev
      ```
    </Note>

    <Tip>
      Add `--watch` while you work to restart your application automatically whenever one of its secrets changes in Infisical.
    </Tip>

    <Accordion title="Injecting secrets into a shell function or alias">
      A start command that is a shell function or an alias can't be called directly after `--`, because it only exists inside your shell. Use the `--command` flag to run it in a shell instead.

      For example, if `custom.sh` defines a `yd` function that runs `yarn dev`:

      ```bash theme={"dark"}
      #!/bin/sh

      yd() {
        yarn dev
      }
      ```

      Source the file and call the function in a single command:

      ```bash theme={"dark"}
      infisical run --env=dev --command="source custom.sh && yd"
      ```

      The `--command` flag is also how you chain commands together, as in `--command="npm run migrate && npm run dev"`.
    </Accordion>

    For every available option, see the [`infisical run`](/docs/cli/commands/run) reference.

    For installation instructions, troubleshooting, and related local workflows such as personal overrides and secret scanning, see the [local development guide](/docs/documentation/guides/local-development).
  </Tab>

  <Tab title="Docker containers">
    Install the Infisical CLI into your Docker image and start your application with it to inject secrets at runtime.

    <Steps>
      <Step title="Install the Infisical CLI in your Dockerfile">
        Install the CLI with the package manager of your base image. The example below targets Alpine; find the commands for other distributions [here](/docs/cli/overview).

        ```dockerfile theme={"dark"}
        RUN apk add --no-cache bash wget && \
            wget -qO- 'https://artifacts-cli.infisical.com/setup.apk.sh' | sh && \
            apk update && apk add infisical
        ```
      </Step>

      <Step title="Start your application with the CLI">
        Set your container start command to run your application through `infisical run`. The CLI fetches your secrets from Infisical and injects them as environment variables.

        ```dockerfile theme={"dark"}
        CMD ["infisical", "run", "--projectId", "<your-project-id>", "--env", "prod", "--", "npm", "run", "start"]
        ```
      </Step>

      <Step title="Authenticate the container">
        Create a [machine identity](/docs/documentation/platform/identities/machine-identities) and pass its access token to the container through the `INFISICAL_TOKEN` environment variable.

        ```bash theme={"dark"}
        docker run --env INFISICAL_TOKEN=$INFISICAL_TOKEN <your-image>
        ```
      </Step>
    </Steps>

    For Docker Compose and `--env-file` workflows, see the [Docker guide](/docs/integrations/platforms/docker).
  </Tab>

  <Tab title="Staging, production & all other use cases">
    In the following steps, we explore how to use the Infisical CLI in a non-local development scenario
    to fetch back environment variables and export them to a file.

    <Steps>
      <Step title="Create a machine identity and obtain credentials for it">
        Follow the steps listed [here](/docs/documentation/platform/identities/universal-auth) to create a machine identity and obtain a **client ID** and **client secret** for it.
      </Step>

      <Step title="Obtain a machine identity access token">
        Run the following command to authenticate with Infisical using the **client ID** and **client secret** credentials from step 1 and set the `INFISICAL_TOKEN` environment variable to the retrieved access token.

        ```bash theme={"dark"}
        export INFISICAL_TOKEN=$(infisical login --method=universal-auth --client-id=<identity-client-id> --client-secret=<identity-client-secret> --silent --plain) # --plain flag will output only the token, so it can be fed to an environment variable. --silent will disable any update messages.
        ```

        The CLI is configured to look out for the `INFISICAL_TOKEN` environment variable, so going forward any command used will be authenticated.

        Alternatively, assuming you have an access token on hand, you can also pass it directly to the CLI using the `--token` flag in conjunction with other CLI commands.

        <Info>
          Keep in mind that the machine identity access token has a limited lifetime. It is recommended to use it only for the duration of the task at hand.
          You can [refresh the token](./commands/token) if needed.
        </Info>
      </Step>

      <Step title="Export environment variables back into a file">
        Finally, export the environment variables from Infisical to a file of choice.

        ```bash theme={"dark"}
        # export variables to a .env file (with export keyword)
        infisical export --format=dotenv-export > .env

        # export variables to a YAML file
        infisical export --format=yaml > secrets.yaml
        ```
      </Step>
    </Steps>
  </Tab>
</Tabs>

<Note>
  Starting with CLI version v0.4.0, you can now choose to log in via Infisical Cloud (US/EU) or your own self-hosted instance by simply running `infisical login` and following the on-screen instructions — no need to manually set the `INFISICAL_API_URL` environment variable.

  For versions prior to v0.4.0, the CLI defaults to US Cloud. To connect to EU Cloud or a self-hosted instance, set the `INFISICAL_API_URL` environment variable to `https://eu.infisical.com` or your custom URL.
</Note>

<Warning>
  ## Domain configuration

  **Important:** If you're not using interactive login, you must configure the domain for **all CLI commands**.

  The CLI defaults to US Cloud ([https://app.infisical.com](https://app.infisical.com)). To connect to **EU Cloud ([https://eu.infisical.com](https://eu.infisical.com))** or a **self-hosted instance**, you must configure the domain in one of the following ways:

  * Use the `INFISICAL_DOMAIN` environment variable
  * Use the `--domain` flag on every command
  * Set the `domain` field in your project's [`.infisical.json`](/docs/cli/project-config)

  When more than one is set, the CLI uses this order of precedence: `--domain` flag, then `INFISICAL_DOMAIN`, then the `domain` field in `.infisical.json`, then the default. The legacy `INFISICAL_API_URL` environment variable is still honored, but `INFISICAL_DOMAIN` takes precedence when both are set.

  <Tabs>
    <Tab title="Use Environment Variable (Recommended)">
      The easiest way to ensure all CLI commands use the correct domain is to set
      the `INFISICAL_DOMAIN` environment variable. This applies the domain
      setting globally to all commands:

      ```bash theme={"dark"}
      # Linux/MacOS
      export INFISICAL_DOMAIN="https://your-domain.infisical.com"

      # Windows PowerShell
      setx INFISICAL_DOMAIN "https://your-domain.infisical.com"
      ```

      Once set, all subsequent CLI commands will automatically use this domain:

      ```bash theme={"dark"}
      # Login with the domain
      infisical login --method=universal-auth --client-id=<client-id> --client-secret=<client-secret> --silent --plain

      # All other commands will also use the same domain automatically
      infisical secrets --projectId <id> --env dev
      ```
    </Tab>

    <Tab title="Use --domain Flag">
      The `--domain` flag can be used to set the domain for a single command. This
      applies the domain setting to the command only:

      ```bash theme={"dark"}
      # Login with domain
      infisical login --domain="https://your-domain.infisical.com" --method=universal-auth --client-id=<client-id> --client-secret=<client-secret> --silent --plain

      # All subsequent commands must also include --domain
      infisical secrets --domain="https://your-domain.infisical.com" --projectId=<id> --env=dev
      ```

      <Note>
        If you use `--domain` during login but forget to include it on subsequent commands, you may encounter authentication errors.
      </Note>
    </Tab>

    <Tab title="Use .infisical.json">
      If your project has a [`.infisical.json`](/docs/cli/project-config) file, you can pin the
      domain to the project by adding a `domain` field. Every CLI command run from the
      project then uses it automatically, with no flag or environment variable needed:

      ```json .infisical.json theme={"dark"}
      {
        "workspaceId": "<workspace-id>",
        "defaultEnvironment": "dev",
        "domain": "https://your-domain.infisical.com"
      }
      ```

      <Note>
        Since `.infisical.json` is usually committed to your repository, the CLI prints a warning naming the host whenever the domain is read from the file, since all requests and credentials are sent there. Only set `domain` to an instance you trust.
      </Note>
    </Tab>
  </Tabs>
</Warning>

<Tip>
  ## Custom request headers

  The Infisical CLI supports custom HTTP headers for requests to servers protected by authentication services such as Cloudflare Access. Configure these headers using the `INFISICAL_CUSTOM_HEADERS` environment variable:

  ```bash theme={"dark"}
  # Syntax: headername1=headervalue1 headername2=headervalue2
  export INFISICAL_CUSTOM_HEADERS="Access-Client-Id=your-client-id Access-Client-Secret=your-client-secret"

  # Execute Infisical commands after setting the environment variable
  infisical secrets
  ```

  This functionality enables secure interaction with Infisical instances that require specific authentication headers.
</Tip>

## History

Your terminal keeps a history with the commands you run. When you create Infisical secrets directly from your terminal, they'll stay there for a while.

For security and privacy concerns, we recommend you to configure your terminal to ignore those specific Infisical commands.

<Accordion title="Ignore commands">
  <Tabs>
    <Tab title="Unix/Linux">
      <Tip>
        `$HOME/.profile` is pretty common but, you could place it under `$HOME/.profile.d/infisical.sh` or any profile file run at login
      </Tip>

      ```bash theme={"dark"}
      cat <<EOF >> $HOME/.profile && source $HOME/.profile

      # Ignoring specific Infisical CLI commands
      DEFAULT_HISTIGNORE=$HISTIGNORE
      export HISTIGNORE="*infisical secrets set*:$DEFAULT_HISTIGNORE"
      EOF
      ```
    </Tab>

    <Tab title="Windows">
      If you're on WSL, then you can use the Unix/Linux method.

      <Tip>
        Here's some [documentation](https://superuser.com/a/1658331) about how to clear the terminal history, in PowerShell and CMD
      </Tip>
    </Tab>
  </Tabs>
</Accordion>

## FAQ

<AccordionGroup>
  <Accordion title="Can I connect the CLI to my self-hosted or non-US Cloud Infisical instance?">
    Yes. The CLI is set to connect to Infisical US Cloud by default, but if you're using EU Cloud or a self-hosted instance you can configure the domain for **all CLI commands**.

    #### Method 1: Use the updated CLI (v0.4.0+)

    Beginning with CLI version V0.4.0, you can choose between logging in through Infisical US Cloud, EU Cloud, or your own self-hosted instance. Simply execute the `infisical login` command and follow the on-screen instructions.

    #### Method 2: Export environment variable

    You can point the CLI to the self-hosted Infisical instance by exporting the environment variable `INFISICAL_DOMAIN` in your terminal. (The legacy `INFISICAL_API_URL` variable still works.)

    <Tabs>
      <Tab title="Linux/MacOs">
        ```bash theme={"dark"}
        # Set the domain
        export INFISICAL_DOMAIN="https://your-self-hosted-infisical.com"

        # For EU Cloud
        export INFISICAL_DOMAIN="https://eu.infisical.com"

        # Remove the setting
        unset INFISICAL_DOMAIN
        ```
      </Tab>

      <Tab title="Windows Powershell">
        ```bash theme={"dark"}
        # Set the domain
        setx INFISICAL_DOMAIN "https://your-self-hosted-infisical.com"

        # For EU Cloud
        setx INFISICAL_DOMAIN "https://eu.infisical.com"

        # Remove the setting
        setx INFISICAL_DOMAIN ""

        # NOTE: Once set, please restart powershell for the change to take effect
        ```
      </Tab>
    </Tabs>

    #### Method 3: Set manually on every command

    If you prefer not to use an environment variable, you must include the `--domain` flag on **every CLI command** you run:

    ```bash theme={"dark"}
    # Login with domain
    infisical login --domain="https://your-domain.infisical.com" --method=oidc-auth --jwt $JWT

    # All subsequent commands must also include --domain
    infisical secrets --domain="https://your-self-hosted-infisical.com" --projectId <id> --env dev
    infisical export --domain="https://your-self-hosted-infisical.com" --format=dotenv-export
    ```

    <Tip>
      **Best Practice:** Use `INFISICAL_DOMAIN` environment variable (Method 2) to avoid having to remember the `--domain` flag on every command. This is especially important in CI/CD pipelines and automation scripts.
    </Tip>
  </Accordion>

  <Accordion title="Can I use the CLI with service tokens?">
    To use Infisical for non local development scenarios, please create a service token. The service token will allow you to authenticate and interact with Infisical. Once you have created a service token with the required permissions, you’ll need to feed the token to the CLI.

    ```bash theme={"dark"}
      infisical export --token=<service-token>
      infisical secrets --token=<service-token>
      infisical run --token=<service-token> -- npm run dev
    ```

    #### Pass via shell environment variable

    The CLI is configured to look for an environment variable named `INFISICAL_TOKEN`. If set, it’ll attempt to use it for authentication.

    ```bash theme={"dark"}
      export INFISICAL_TOKEN=<service-token>
    ```
  </Accordion>
</AccordionGroup>
