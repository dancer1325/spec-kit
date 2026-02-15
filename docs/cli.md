# 🔧 Specify CLI Reference

## `specify` commands

| Command | Description                                                                                                                                             |
| ------- |---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `init`  | FROM the latest template -> initialize a NEW specify project                                                                                            |
| `check` | Check for installed tools (`git`, `claude`, `gemini`, `code`/`code-insiders`, `cursor-agent`, `windsurf`, `qwen`, `opencode`, `codex`, `shai`, `qoder`) |

### `specify init` arguments & options

| Argument/Option        | Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|------------------------| -------- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `<project-name>`       | Argument | if you use `--here` OR `.` -> OPTIONAL                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `--ai`                 | Option   | AI assistant to use: <br/> &nbsp;&nbsp; `claude` <br/> &nbsp;&nbsp; `gemini` <br/> &nbsp;&nbsp; `copilot` <br/> &nbsp;&nbsp; `cursor-agent` <br/> &nbsp;&nbsp; `qwen` <br/> &nbsp;&nbsp; `opencode` <br/> &nbsp;&nbsp; `codex` <br/> &nbsp;&nbsp; `windsurf` <br/> &nbsp;&nbsp; `kilocode` <br/> &nbsp;&nbsp; `auggie` <br/> &nbsp;&nbsp; `roo` <br/> &nbsp;&nbsp; `codebuddy` <br/> &nbsp;&nbsp; `amp` <br/> &nbsp;&nbsp; `shai` <br/> &nbsp;&nbsp; `q` <br/> &nbsp;&nbsp; `bob` <br/> &nbsp;&nbsp; `qoder` |
| `--script`             | Option   | Script variant to use: <br/> &nbsp;&nbsp; `sh` (bash/zsh) <br/> &nbsp;&nbsp; `ps` (PowerShell)                                                                                                                                                                                                                                                                                                                                                                                                               |
| `--ignore-agent-tools` | Flag     | Skip checks for AI agent tools <br/> _Example:_ if you choose claude -> skip checking you have installed Claude Code <br/> use cases: CI/CD                                                                                                                                                                                                                                                                                                                                                                  |
| `--no-git`             | Flag     | Skip git repository initialization                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `--here`               | Flag     | Initialize project \| current directory                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `--force`              | Flag     | \| current & NON empty directory, force (== skip confirmation) merge/overwrite <br/> use cases: CI/CD, re-initialize                                                                                                                                                                                                                                                                                                                                                                                         |
| `--skip-tls`           | Flag     | \| download template from Github, skip SSL/TLS verification (❌NOT recommended❌) <br/> use cases: corporate proxies                                                                                                                                                                                                                                                                                                                                                                                           |
| `--debug`              | Flag     | enable detailed debug                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `--github-token`       | Option   | \| download template from Github, provide GitHub personal access token for API requests OR set `GH_TOKEN`/`GITHUB_TOKEN` env variable <br/> use cases: private templates, corporate environments, CI/CD                                                                                                                                                                                                                                                                                                      |

## `/speckit.*` -- slash commands --

* requirements
  * have run `specify init`
* uses
  * 💡| your AI coding agent chat💡

### Core Commands

* == SDD workflow's essential commands 

| Command                 | Description                                                            |
| ----------------------- |------------------------------------------------------------------------|
| `/speckit.constitution` | Create OR update project governing principles & development guidelines |
| `/speckit.specify`      | Define what you want to build (requirements & user stories)            |
| `/speckit.plan`         | Create technical implementation plans / you choose tech stack          |
| `/speckit.tasks`        | Generate actionable task lists -- for -- implementation                |
| `/speckit.implement`    | Execute ALL tasks / build the feature -- based on the -- plan          |

### OPTIONAL Commands

* allows
  * enhance quality and validation

| Command              | Description                                                                                                                        |
| -------------------- |------------------------------------------------------------------------------------------------------------------------------------|
| `/speckit.clarify`   | Clarify underspecified areas <br/> recommended uses: BEFORE `/speckit.plan`                                                        |
| `/speckit.analyze`   | Cross-artifact consistency & coverage analysis <br/> uses: [AFTER `/speckit.tasks`, BEFORE `/speckit.implement`]                   |
| `/speckit.checklist` | Generate custom quality checklists / validate requirements completeness, clarity, and consistency |

## Environment Variables

| Variable          | Description                                                                                                                                                 |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SPECIFY_FEATURE` | override feature detection <br/> &nbsp;&nbsp; \| non-Git repositories <br/> &nbsp;&nbsp; \| not use Git branches <br/> requirements: BEFORE `/speckit.plan` |
