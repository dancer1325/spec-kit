# Installation Guide

## ⚠️Prerequisites⚠️

- OS
  - Linux
  - macOS
  - Windows
    - RIGHT NOW (BUT NOT from the scratch)
      - Reason:🧠PowerShell scripts were NOT supported🧠
- [AI coding agent](supportedAIAgents.md)
- [uv](https://docs.astral.sh/uv/) 
  - Reason:🧠package management🧠
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

## Initialize a NEW Project

```bash
# 1. <PROJECT_NAME>
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>

# 2. | CURRENT directory
uvx --from git+https://github.com/github/spec-kit.git specify init .

# 3. --here   == 2.
uvx --from git+https://github.com/github/spec-kit.git specify init --here
```

### + specify AI Agent -- via -- `--ai`

```bash
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
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --script sh
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --script ps
```

### + ignore Agent Tools check -- via -- `--ignore-agent-tools`

* == get the templates / ❌NO check if you fulfill the [prerequisites](#prerequisites)❌
  * _Example:_ if you do NOT have AI agent -> NO error

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <project_name> --ai claude --ignore-agent-tools
```

### verification

* | AFTER initialization, 
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
