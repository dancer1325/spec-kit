# Installation Guide

## ⚠️Prerequisites⚠️

* OS
  * Linux
  * macOS
  * Windows
    * RIGHT NOW (BUT NOT from the scratch)
      * Reason:🧠PowerShell scripts were NOT supported🧠
* [AI coding agent](supportedAIAgents.md)
* [uv](https://docs.astral.sh/uv/) 
  * Reason:🧠package management🧠
* [Python 3.11+](https://www.python.org/downloads/)
* [Git](https://git-scm.com/downloads)

## how to install?

TODO: 
> [!IMPORTANT]
> The only official, maintained packages for Spec Kit come from the [github/spec-kit](https://github.com/github/spec-kit) GitHub repository. Any packages with the same name available on PyPI (e.g. `specify-cli` on pypi.org) are **not** affiliated with this project and are not maintained by the Spec Kit maintainers. For normal installs, use the GitHub-based commands shown below. For offline or air-gapped environments, locally built wheels created from this repository are also valid.

### Persistent Installation (Recommended)

Install once and use everywhere. Replace `vX.Y.Z` with a tag from [Releases](https://github.com/github/spec-kit/releases):

> [!NOTE]
> The command below requires **[uv](https://docs.astral.sh/uv/)**. If you see `command not found: uv`, [install uv first](./install/uv.md).

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

Then initialize a project:

```bash
specify init <PROJECT_NAME> --integration copilot
```

### One-time Usage

Run directly without installing — see the [One-time usage (uvx)](install/one-time.md) guide.

### Alternative Package Managers

- **pipx** — see the [pipx installation guide](install/pipx.md)
- **Enterprise / Air-Gapped** — see the [air-gapped installation guide](install/air-gapped.md)

## Initialize a NEW Project

```bash
# 1. <PROJECT_NAME>
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>

# 2. | CURRENT directory
uvx --from git+https://github.com/github/spec-kit.git specify init .

# 3. --here   == 2.
uvx --from git+https://github.com/github/spec-kit.git specify init --here
```

### + specify integration

Interactive terminals prompt you to choose a coding agent integration during initialization. Non-interactive sessions, such as CI or piped runs, default to GitHub Copilot unless you pass `--integration`.

You can proactively specify your coding agent integration during initialization:

```bash
specify init <project_name> --integration claude
specify init <project_name> --integration gemini
specify init <project_name> --integration copilot
specify init <project_name> --integration codebuddy
specify init <project_name> --integration pi
```

### + specify AI Agent -- via -- `--ai`

```bash
#TODO: do I need uvx --from git+https://github.com/github/spec-kit.git ?
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai claude
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai gemini
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai copilot
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai codebuddy
```

### + specify script type (Shell vs PowerShell) -- via -- `--script`

* automation scripts
  * support
    * Bash (`.sh`)
    * PowerShell (`.ps1`)
  * AUTOMATICALLY choose -- based on -- OS
    * Windows: `ps`
    * Rest: `sh`
  * if you want to specify -> pass `--script sh|ps`

```bash
#TODO: do I need uvx --from git+https://github.com/github/spec-kit.git ? 
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --script sh
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --script ps
```

### + ignore Agent Tools check -- via -- `--ignore-agent-tools`

* == get the templates / ❌NO check if you fulfill the [prerequisites](#prerequisites)❌
  * _Example:_ if you do NOT have AI agent -> NO error

```bash
specify init <project_name> --integration claude --ignore-agent-tools
```

### verification

* | AFTER initialization, 
  * `specify version`
    * check the installed Specify version 
  * run `specify self check` PERIODICALLY
    * Reason:🧠check whether a NEWER release is AVAILABLE🧠
    * 👀read-only👀
      * == NEVER modify your installation
      * ONCE you want to upgrade -> follow the [upgrade guide](./upgrade.md)
  * commands / AVAILABLE | your AI agent
    - `/speckit.specify` 
      - Create specifications
    - `/speckit.plan` 
      - Generate implementation plans  
    - `/speckit.tasks` 
      - Break down into actionable tasks
  * ".specify/scripts/"
    * == ALL `.sh` & `.ps1` scripts

## Troubleshooting

### Enterprise / Air-Gapped Installation

If your environment blocks access to PyPI or GitHub, see the [Enterprise / Air-Gapped Installation](install/air-gapped.md) guide for step-by-step instructions on creating portable wheel bundles.

### Git Credential Manager | Linux

* TODO: If you're having issues with Git authentication on Linux, you can install Git Credential Manager:

```bash
#!/usr/bin/env bash
set -e
echo "Downloading Git Credential Manager v2.6.1..."
wget https://github.com/git-ecosystem/git-credential-manager/releases/download/v2.6.1/gcm-linux_amd64.2.6.1.deb
echo "Installing Git Credential Manager..."
sudo dpkg -i gcm-linux_amd64.2.6.1.deb
echo "Configuring Git to use GCM..."
git config --global credential.helper manager
echo "Cleaning up..."
rm gcm-linux_amd64.2.6.1.deb
```
