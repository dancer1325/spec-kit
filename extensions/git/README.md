# Git Branching Workflow Extension

* Git repository
  * == self-contained module /
    * built-in extension
    * provide
      * repository initialization / 
        * CONFIGURABLE commit messages
      * feature branch creation
        * 's naming
          * sequential, OR
            * _Example:_ `001-feature-name`
          * timestamp
            * _Example:_ `20260319-143022-feature-name`
        * 's template for branch namespaces
          * OPTIONAL
      * branch naming validation
      * Git remote detection
        * uses
          * issue creation -- through -- `/speckit.taskstoissues`
      * AFTER `/speckit.*`, auto-commit | Git repository

## Commands

| Command                  | Description                                                                |
|--------------------------|----------------------------------------------------------------------------|
| `speckit.git.initialize` | Initialize a Git repository -- with a -- configurable commit message       |
| `speckit.git.feature`    | Create a feature branch / 's name: sequential OR timestamp numbering       |
| `speckit.git.validate`   | Validate CURRENT branch follows feature branch naming conventions          |
| `speckit.git.remote`     | Detect Git remote URL -- for -- GitHub integration                         |
| `speckit.git.commit`     | Auto-commit changes (configurable per-command enable/disable and messages) |

## Hooks

| Event                  | Command                  | Optional  | Description                                       |
|------------------------|--------------------------|-----------|---------------------------------------------------|
| `before_constitution`  | `speckit.git.initialize` | No        | Init git repo before constitution                 |
| `before_specify`       | `speckit.git.feature`    | No        | BEFORE specification, create feature branch       |
| `before_clarify`       | `speckit.git.commit`     | Yes       | Commit outstanding changes before clarification   |
| `before_plan`          | `speckit.git.commit`     | Yes       | Commit outstanding changes before planning        |
| `before_tasks`         | `speckit.git.commit`     | Yes       | Commit outstanding changes before task generation |
| `before_implement`     | `speckit.git.commit`     | Yes       | Commit outstanding changes before implementation  |
| `before_checklist`     | `speckit.git.commit`     | Yes       | Commit outstanding changes before checklist       |
| `before_analyze`       | `speckit.git.commit`     | Yes       | Commit outstanding changes before analysis        |
| `before_taskstoissues` | `speckit.git.commit`     | Yes       | Commit outstanding changes before issue sync      |
| `after_constitution`   | `speckit.git.commit`     | Yes       | Auto-commit after constitution update             |
| `after_specify`        | `speckit.git.commit`     | Yes       | Auto-commit after specification                   |
| `after_clarify`        | `speckit.git.commit`     | Yes       | Auto-commit after clarification                   |
| `after_plan`           | `speckit.git.commit`     | Yes       | Auto-commit after planning                        |
| `after_tasks`          | `speckit.git.commit`     | Yes       | Auto-commit after task generation                 |
| `after_implement`      | `speckit.git.commit`     | Yes       | Auto-commit after implementation                  |
| `after_checklist`      | `speckit.git.commit`     | Yes       | Auto-commit after checklist                       |
| `after_analyze`        | `speckit.git.commit`     | Yes       | Auto-commit after analysis                        |
| `after_taskstoissues`  | `speckit.git.commit`     | Yes       | Auto-commit after issue sync                      |

## Configuration

Configuration is stored in `.specify/extensions/git/git-config.yml`:

```yaml
# Branch numbering strategy: "sequential" or "timestamp"
branch_numbering: sequential

# Optional branch name template. Leave empty for the default "{number}-{slug}".
# Supported tokens: {author}, {app}, {number}, {slug}; {slug} must not appear
# before {number}, and the final path segment must start with {number}-.
# Example for monorepos: "{author}/{app}/{number}-{slug}"
branch_template: ""

# Optional shorthand namespace. Leave empty to use branch_template/default behavior.
# Example: "features/{app}" expands to "features/{app}/{number}-{slug}"
branch_prefix: ""

# Custom commit message for git init
init_commit_message: "[Spec Kit] Initial commit"

# Commit message style for auto-commit hooks: "fixed" (default) uses the
# messages below; "conventional" asks the agent to generate a Conventional
# Commit message (e.g. "feat: add OAuth spec") from the diff instead.
commit_style: fixed

# Auto-commit per command (all disabled by default)
# Example: enable auto-commit after specify
auto_commit:
  default: false
  after_specify:
    enabled: true
    message: "[Spec Kit] Add specification"
```

`{author}` is derived from Git config and sanitized for branch names
`{app}` is derived from the Spec Kit init directory name
* Custom templates must not put `{slug}` before `{number}`, and must put `{number}-` at the start of the final path segment so generated names remain valid feature branches
* For a monorepo project at `apps/web/.specify/`, a template such as `{author}/{app}/{number}-{slug}` produces branches like `jdoe/web/008-guided-tour`.

For simple namespace-only customization, `branch_prefix` is also accepted as a shorthand and expands to `<branch_prefix>/{number}-{slug}`.

## how to install this extension?

```bash
# NO require network connectivity
#   Reason:🧠built-in extension🧠
specify extension add git
```

## how to enable / disable?

```bash
# Disable the git extension
specify extension disable git

# Re-enable it
specify extension enable git
```

## Graceful Degradation

When Git is not installed or the directory is not a Git repository:
- Spec directories are still created under `specs/`
- Branch creation is skipped with a warning
- Branch validation is skipped with a warning
- Remote detection returns empty results

## Scripts

The extension bundles cross-platform scripts:

- `scripts/bash/create-new-feature-branch.sh` — Bash implementation (branch creation only)
- `scripts/bash/git-common.sh` — Shared Git utilities (Bash)
- `scripts/powershell/create-new-feature-branch.ps1` — PowerShell implementation (branch creation only)
- `scripts/powershell/git-common.ps1` — Shared Git utilities (PowerShell)
