# Core Commands -- `specify <COMMAND_NAME>` --

* allows
  * manage Spec Kit projects

## `specify init` -- initialize a Specify Project --

```bash
specify init [<project_name>]
```

* add
  * directory structure + templates + scripts + AI coding agent integration files 
* [source code](/spec-kit/src/specify_cli/commands/init.py)'s `def init(`

| Argument/Option          | Type     | Description                                                                                                                                                                                                   |
|--------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `<project-name>`         | Argument | if you use `--here` OR `.` -> OPTIONAL                                                                                                                                                                        |
| `--script sh\|ps`        | Option   | == script variant to use <br/> &nbsp;&nbsp; `sh` (bash/zsh) <br/> &nbsp;&nbsp; `ps` (PowerShell) <br/> AUTOMATICALLY chosen -- based on -- OS <br/> &nbsp;&nbsp; Windows: `ps` <br/> &nbsp;&nbsp; Rest: `sh`  |
| `--ignore-agent-tools`   | Flag     | Skip checks for AI agent tools <br/> _Example:_ if you choose claude -> skip checking you have installed Claude Code <br/> use cases: CI/CD                                                                   |
| `--no-git`               | Flag     | Skip git repository initialization                                                                                                                                                                            |
| `--here`                 | Flag     | Initialize project \| CURRENT directory                                                                                                                                                                       |
| `--force`                | Flag     | \| current & NON empty directory, force (== skip confirmation) merge/overwrite <br/> use cases: CI/CD, re-initialize                                                                                          |
| `--integration <key>`    | Option   | [here](integrations.md) <br/> if you do NOT specify it -> chosen \| prompt                                                                                                                                    |
| `--integration-options`  | Option   | Options for the integration (e.g. `--integration-options="--skills"`)                                                                                                                                         |
| `--preset <id>`          | Option   | install a preset                                                                                                                                                                                              |
| `--branch-numbering`     | Option   | Branch numbering strategy: `sequential` (001, 002, …) or `timestamp` (YYYYMMDD-HHMMSS)                                                                                                                        |

* | Github SpecKit v0.10.0-
  * by default,
    * has git extension
* | Github SpecKit v0.10.0+
  * if you want git extension -> you need to run `specify extension add git`

| Variable          | Description                                                                                                                                                                                         |
| ----------------- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SPECIFY_FEATURE` | \| non-Git repositories <br/> &nbsp;&nbsp; override feature detection <br/> \| NOT use Git branches <br/> &nbsp;&nbsp; set to the feature directory name <br/> requirements: BEFORE `/speckit.plan` |

## `specify check` -- check installed tools

```bash
specify check
```

* required tools
  * git
  * CLI-based AI coding agents

## `specify self check` -- check specify itself

```bash
specify self check
```

* check if there are newer specify version
* ⚠️read-only⚠️
  * == ❌NEVER modify your installation❌
  * if you want to upgrade -> [upgrade guide](../upgrade.md)

## `specify version` -- Version Information

```bash
specify version [OPTIONS]
```

* displays the
  * Spec Kit CLI version
  * Python version
  * platform
  * architecture

* `[OPTIONS]`
  * `--features`
    * 's return:
      * local CLI capabilities
  * `--json`
    * use cases
      * scripts
      * coding agents

* ALTERNATIVES
  * `specify --version` OR `specify -v`
