> ## Documentation Index
> Fetch the complete documentation index at: https://infisical.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Install

> Infisical's CLI is one of the best ways to manage environments and secrets. Install it here

<Warning>
  **Action required for Linux users.** The Infisical CLI Linux package repository moved from Cloudsmith to `artifacts-cli.infisical.com`. The Cloudsmith repository stopped serving on **September 16, 2026**. Machines still pointed at the old URL will fail to install or update. See the [migration guide](/docs/cli/cloudsmith-migration) for step-by-step instructions.
</Warning>

The Infisical CLI is a powerful command line tool that can be used to retrieve, modify, export and inject secrets into any process or application as environment variables.
You can use it across various environments, whether it's local development, CI/CD, staging, or production.

## Installation

Install the CLI with the package manager for your operating system.

<CodeGroup>
  ```bash macOS theme={"dark"}
  brew install infisical/get-cli/infisical
  ```

  ```bash Windows (winget) theme={"dark"}
  winget install infisical
  ```

  ```bash Windows (Scoop) theme={"dark"}
  scoop bucket add org https://github.com/Infisical/scoop-infisical.git
  scoop install infisical
  ```

  ```bash npm theme={"dark"}
  npm install -g @infisical/cli
  ```

  ```bash Debian/Ubuntu theme={"dark"}
  curl -1sLf 'https://artifacts-cli.infisical.com/setup.deb.sh' | sudo -E bash
  sudo apt-get update && sudo apt-get install -y infisical
  ```

  ```bash RedHat/CentOS/Amazon Linux theme={"dark"}
  curl -1sLf 'https://artifacts-cli.infisical.com/setup.rpm.sh' | sudo -E bash
  sudo yum install infisical
  ```

  ```bash Alpine theme={"dark"}
  apk add --no-cache bash sudo wget
  wget -qO- 'https://artifacts-cli.infisical.com/setup.apk.sh' | sudo sh
  apk update && sudo apk add infisical
  ```

  ```bash Arch Linux theme={"dark"}
  yay -S infisical-bin
  ```
</CodeGroup>

<Tip>
  When you install the CLI in a production environment, pin it to a specific version so that the version stays the same across reinstalls. [View versions](https://github.com/Infisical/cli/releases)
</Tip>

## Update the CLI

<CodeGroup>
  ```bash macOS theme={"dark"}
  brew update && brew upgrade infisical
  ```

  ```bash Windows (Scoop) theme={"dark"}
  scoop update infisical
  ```

  ```bash npm theme={"dark"}
  npm update -g @infisical/cli
  ```
</CodeGroup>

On Linux, update the CLI with the package manager you installed it with.

## Quick usage guide

<Card color="#00A300" href="./usage">
  Now that you have the CLI installed on your system, follow this guide to make the best use of it
</Card>
