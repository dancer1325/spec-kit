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

| Argument/Option         | Type     | Description                                                                                                                                                                                                                      |
|-------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `<project-name>`        | Argument | if you use `--here` OR `.` -> OPTIONAL                                                                                                                                                                                           |
| `--script sh\|ps\|py`   | Option   | == script variant to use <br/> &nbsp;&nbsp; `sh` (bash/zsh) <br/> &nbsp;&nbsp; `ps` (PowerShell) <br/> `py` (Python) <br/> AUTOMATICALLY chosen -- based on -- OS <br/> &nbsp;&nbsp; Windows: `ps` <br/> &nbsp;&nbsp; Rest: `sh` |
| `--ignore-agent-tools`  | Flag     | Skip checks for AI agent tools <br/> _Example:_ if you choose claude -> skip checking you have installed Claude Code <br/> use cases: CI/CD                                                                                      |
| `--here`                | Flag     | Initialize project \| CURRENT directory                                                                                                                                                                                          |
| `--force`               | Flag     | \| current & NON empty directory, force (== skip confirmation) merge/overwrite <br/> use cases: CI/CD, re-initialize                                                                                                             |
| `--integration <key>`   | Option   | [here](integrations.md) <br/> if you do NOT specify it -> chosen \| prompt                                                                                                                                                       |
| `--integration-options` | Option   | Options for the integration (e.g. `--integration-options="--skills"`)                                                                                                                                                            |
| `--preset <id>`         | Option   | install a preset                                                                                                                                                                                                                 |

* | Github SpecKit v0.10.0-
  * by default,
    * has git extension
* | Github SpecKit v0.10.0+
  * if you want git extension -> you need to run `specify extension add git`

| Variable          | Description                                                                                                                                                                                         |
| ----------------- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SPECIFY_FEATURE` | \| non-Git repositories <br/> &nbsp;&nbsp; override feature detection <br/> \| NOT use Git branches <br/> &nbsp;&nbsp; set to the feature directory name <br/> requirements: BEFORE `/speckit.plan` |
| `SPECIFY_INIT_DIR` | Target a member project from outside its directory (e.g. a monorepo root) without `cd`, for non-interactive / CI use. Set it to the **project root** — the directory *containing* `.specify/` (relative paths resolve against the current directory). The path must exist and contain `.specify/`, otherwise the command errors and does **not** fall back to the current directory. Resolved once in the core root helper (`get_repo_root` in Bash, `Get-RepoRoot` in PowerShell), so it is honored by the core feature scripts (`/speckit.plan`, `/speckit.tasks`, …) and the Git extension's feature-branch creation, which inherit it. The `specify` CLI applies the **same** validation rules to every project-scoped subcommand (`specify integration …`, `specify extension …`, `specify workflow …`, `specify preset …`, and the rest that operate on a `.specify/` project), so those can target a member project too. When unset, Bash/PowerShell helpers keep their existing upward search; the `specify` CLI keeps its project-scoped resolver cwd-only unless a command explicitly defines broader detection (for example, bundle commands). |
| `SPECIFY_FEATURE_DIRECTORY` | Override the active feature directory *within* the resolved project (takes precedence over `.specify/feature.json`). Relative paths resolve under the project root. Combine with `SPECIFY_INIT_DIR` to pick both the project and the feature non-interactively. |

> **Two resolution axes.** `SPECIFY_INIT_DIR` selects the **project** (which directory contains `.specify/`); `SPECIFY_FEATURE_DIRECTORY` / `.specify/feature.json` select the **feature** within that project. They are independent — project first, then feature.

> **Symlinked project roots.** `SPECIFY_INIT_DIR` relocates *where* the project is, not *how* a command treats symlinks: each command keeps its existing cwd-path stance. Commands that traverse and write project files through broad input paths (`bundle`, `workflow run <file>`) refuse a symlinked `.specify/` to preserve write confinement. Other project-scoped commands keep their existing behavior when `SPECIFY_INIT_DIR` points at a project root, which may include following a symlinked `.specify/`.

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
