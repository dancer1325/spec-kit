# Spec Kit Integration

* Spec Kit Integration
  * == adapter / 
    * allows
      * connecting Spec Kit -- to -- >= 1 AI coding agent | 1! project
        * ⚠️if you want >1 -> you need Spec Kit v0.8.5⚠️
        * == Spec Kit's core templates are transformed -- to -- AI coding agent's specific format & location
    * identified -- by -- 1! key
    * types
      * CLI required
        * CLI-based
          * _Examples:_ claude, gemini, codex
          * == ⚠️requires ⚠️
            * install the CLI tool
        * IDE-based
          * _Examples:_ windsurf, cursor-agent, copilot
          * == ⚠️requires⚠️
            * IDE/extension
      * MULTI-install safe
        * == dedicated agent root + dedicated command directory + dedicated context file
          * [source code](/spec-kit/src/specify_cli/integrations)
          * integrations / share a context file OR command directory -- with -- ANOTHER integration -> require
            * dynamic install paths, OR
              * _Example:_ `--commands-dir`
            * merge shared tool settings / by default, NOT declared safe
    * 's output
      * command files | specific AI coding agent's directory
      * specific AI coding agent's context file
        * _Examples:_
          * CLAUDE.md
          * GEMINI.md
          * ...
      * specific scripts | ".specify/scripts"

* ".specify/integration.json"
  * [source code](/spec-kit/src/specify_cli/integration_state.py)
  * schema
    * `.integration`
      * == legacy field /
        * == alias -- for the -- default integration
    * `.installed_integrations`
      * == ALL installed integrations
    * `.integration_settings`
      * == runtime settings / EACH integration

    ```json
    {
      "integration_state_schema": 1,
      "integration": "claude",
      "default_integration": "claude",
      "installed_integrations": ["claude", "gemini"],
      "integration_settings": {
        "claude": { "script": "sh" },
        "gemini": { "script": "sh" }
      }
    }
    ```

## Catalog

* schema
  * [source code](../src/specify_cli/extensions.py)

  ```json
  {
    "schema_version": "1.0",
    "updated_at": "2026-04-08T00:00:00Z",
    "catalog_url": "https://...",
    "integrations": {
      "my-agent": {
        "id": "my-agent",
        "name": "My Agent",
        "version": "1.0.0",
        "description": "Integration for My Agent",
        "author": "my-org",
        "repository": "https://github.com/my-org/speckit-my-agent",
        "tags": ["cli"]
      }
    }
  }
  ```

* enables | Spec Kit
  * discovery of AI agent integrations
  * versioning of AI agent integrations
  * distribution of AI agent integrations 

* catalog's priority (== FIRST match wins)
  1. **Environment variable** 
     * `SPECKIT_INTEGRATION_CATALOG_URL` 
       * overrides ALL catalogs -- with -- 1 URL
  2. **Project config**
     * `.specify/integration-catalogs.yml` | project root
  3. **User config** 
     * `~/.specify/integration-catalogs.yml` | user home directory
  4. **Built-in defaults** 
     * `catalog.json` + `catalog.community.json`

### [Built-In Catalog](catalog.json) 

* maintained -- by the -- core team
* ALWAYS installable

### [Community Catalog](catalog.community.json)

* if you want to use -> install it -- from the -- source repositories

## CLI Commands

```bash
# display
#   AVAILABLE integrations
#   currently installed
#   CLI-required OR IDE-based
#   whether is multi-install safe
#   if there are >1 integrations installed -> marks the default integration SEPARATELY 
# --catalog
#   display FULL catalog (built-in + community)
specify integration list

# Install an integration
specify integration install copilot

# Upgrade the current integration (diff-aware)
specify integration upgrade

# Upgrade with force (overwrite modified files)
specify integration upgrade --force
```

### how to add integrations | community catalog?

* [here](CONTRIBUTING.md)

### how to install an integration | CURRENT project?

```bash
specify integration install <key> [OPTION]
```

| Option                   | Description                                                                                |
| ------------------------ |--------------------------------------------------------------------------------------------|
| `--script sh\|ps`        | == Script type <br/> `sh` (bash/zsh) OR `ps` (PowerShell)                                  |
| `--force`                | force to install alongside integrations / are NOT declared multi-install safe              |
| `--integration-options`  | Integration-specific options (e.g. `--integration-options="--commands-dir .myagent/cmds"`) |

* if there is ALREADY ANOTHER integration installed ->
  * ⚠️ONLY if ALL involved integrations are multi-install safe -> the command proceeds AUTOMATICALLY⚠️
    * OTHERWISE,
      * `specify integration install ... --force`, OR
      * `specify integration switch`
  * ❌NOT change the default integration❌
    * ⚠️if you want to change the default integration -> `specify integration use <key>`⚠️
* if the installation
  * fails -> AUTOMATICALLY rolls back -- to a -- clean state
  * NOT ALLOWED because there is ALREADY installed agent -> [upgrade Spec Kit](../docs/upgrade.md)

* | start a NEW project, you can install DIRECTLY a specific agent -> [`specify init <project> --integration <key>`](../docs/cli.md)

### how to uninstall an integration?

```bash
specify integration uninstall [<key>]
# [<key>]
#   == OPTIONAL
#     if you do NOT specify -> uninstall the default one
```

| Option    | Description                                      | 
| --------- |--------------------------------------------------|
| `--force` | even if they have been modified -> remove files  |

TODO: 
Spec Kit tracks every file created during install along with a SHA-256 hash of the original content:

- **Unmodified files** are removed automatically.
- **Modified files** (where you've made manual edits) are preserved so your customizations are not lost.
- Use `--force` to remove all integration files regardless of modifications.

Files you've modified are preserved automatically
* Only unmodified files (matching their original SHA-256 hash) are removed
* Use `--force` to override this.

### how to switch -- to a -- DIFFERENT integration?

```bash
specify integration switch <key>
```

| Option                   | Description                                                                                                                                           |
| ------------------------ |-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--script sh\|ps`        | Script type: `sh` (bash/zsh) or `ps` (PowerShell)                                                                                                     |
| `--force`                | Force removal of modified files during uninstall; when the target is already installed, overwrite managed shared templates while changing the default |
| `--integration-options`  | Options for the target integration when it is not already installed                                                                                   |

If the target integration is not already installed, equivalent to running `uninstall` followed by `install` in a single step
In this mode, `--force` controls whether modified files from the removed integration are deleted
If the target integration is already installed, 
`switch` only changes the default integration, like `use`;
in this mode, `--force` controls whether managed shared templates are overwritten while the default changes
`--integration-options` is rejected for already-installed targets because changing integration options
requires reinstalling managed files; run `upgrade <key> --integration-options ...` first, then `use <key>`.

Files you've modified are preserved automatically
* Only unmodified files (matching their original SHA-256 hash) are removed
* Use `--force` to override this.

* Use `switch` when you want to replace the current default with another integration; if the target is already installed,
  `switch` behaves like `use`.

### how to use an installed Integration?

```bash
specify integration use <key>
```

| Option    | Description                                         |
| --------- | --------------------------------------------------- |
| `--force` | Overwrite managed shared templates while changing the default |

Sets the default integration without uninstalling any other installed integrations. This also refreshes managed shared templates so command references match the new default integration's invocation style. Modified or untracked shared templates are preserved unless `--force` is used.

### how to upgrade an integration?

```bash
specify integration upgrade [<key>]
```

| Option                   | Description                                                              |
| ------------------------ | ------------------------------------------------------------------------ |
| `--force`                | Overwrite files even if they have been modified                          |
| `--script sh\|ps`        | Script type: `sh` (bash/zsh) or `ps` (PowerShell)                        |
| `--integration-options`  | Options for the integration                                              |

Reinstalls an installed integration with updated templates and commands (e.g., after upgrading Spec Kit)
Defaults to the default integration; if a key is provided, it must be one of the installed integrations
Detects locally modified files and blocks the upgrade unless `--force` is used
Stale files from the previous install that are no longer needed are removed automatically
* Shared templates stay aligned with the default integration even when upgrading a non-default integration.

Use `upgrade` when you've upgraded Spec Kit and want to refresh an installed integration's managed files

## Integration Descriptor -- integration.yml --

* documents the integration's
  * metadata
  * requirements
  * provided commands/scripts
* [source code](/spec-kit/src/specify_cli/integrations/catalog.py)'s `IntegrationDescriptor`
* uses
  * ⚠️[community integrations](catalog.community.json)⚠️
    * Reason:🧠built-in are -- based on -- programmatically🧠

## Integration-specific Options -- `--integration-options` --

Some integrations accept additional options via `--integration-options`

| Integration | Option              | Description                                                  |
| ----------- | ------------------- |--------------------------------------------------------------|
| `generic`   | `--commands-dir`    | Required  Directory for command files                        |
| `kimi`      | `--migrate-legacy`  | Migrate legacy dotted skill directories to hyphenated format |

Example:

```bash
specify integration install generic --integration-options="--commands-dir .myagent/cmds"
```
