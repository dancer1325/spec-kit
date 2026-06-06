# Spec Kit Integration

* allows
  * connecting Spec Kit -- to -- >= 1 AI coding agent | 1! project
    * ⚠️if you want >1 -> you need Spec Kit v0.8.5⚠️

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

## Integration Descriptor -- integration.yml --

* documents the integration's
  * metadata
  * requirements
  * provided commands/scripts
* [source code](/spec-kit/src/specify_cli/integrations/catalog.py)'s `IntegrationDescriptor`
* uses
  * ⚠️[community integrations](catalog.community.json)⚠️
    * Reason:🧠built-in are -- based on -- programmatically🧠

### MANDATORY fields

| Field            | Type   | Description                      |
|------------------|--------|----------------------------------|
| `schema_version` | string | Must be `"1.0"`                  |
| `requires`       | object | MINIMUM requirements             |
| `provides`       | object | PROVIDED commands & scripts      |
| `integrations`   | object | Map of integration ID → metadata |

### `.integration`

| Field         | Type | Required  | Description                                  |
|---------------|------|-----------|----------------------------------------------|
| `id`          | string | Yes       | Unique ID (lowercase alphanumeric + hyphens) |
| `name`        | string | Yes       | Human-readable display name                  |
| `version`     | string | Yes       | PEP 440 version (e.g., `1.0.0`, `1.0.0a1`)   |
| `description` | string | Yes       | One-line description                         |
| `author`      | string | No        | Author name or organization                  |
| `repository`  | string | No        | Source repository URL                        |
| `tags`        | array | No        | Searchable tags (e.g., `["cli", "ide"]`)     |

## how to add integrations | community catalog?

* [here](CONTRIBUTING.md)

## how to install an integration | CURRENT project?

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

## Uninstall an Integration

```bash
specify integration uninstall [<key>]
```

| Option    | Description                                         |
| --------- | --------------------------------------------------- |
| `--force` | Remove files even if they have been modified         |

Uninstalls the current integration (or the specified one). Spec Kit tracks every file created during install along with a SHA-256 hash of the original content:

- **Unmodified files** are removed automatically.
- **Modified files** (where you've made manual edits) are preserved so your customizations are not lost.
- Use `--force` to remove all integration files regardless of modifications.

## Switch to a Different Integration

```bash
specify integration switch <key>
```

| Option                   | Description                                                              |
| ------------------------ | ------------------------------------------------------------------------ |
| `--script sh\|ps`        | Script type: `sh` (bash/zsh) or `ps` (PowerShell)                        |
| `--force`                | Force removal of modified files during uninstall; when the target is already installed, overwrite managed shared templates while changing the default |
| `--integration-options`  | Options for the target integration when it is not already installed      |

If the target integration is not already installed, equivalent to running `uninstall` followed by `install` in a single step. In this mode, `--force` controls whether modified files from the removed integration are deleted. If the target integration is already installed, `switch` only changes the default integration, like `use`; in this mode, `--force` controls whether managed shared templates are overwritten while the default changes. `--integration-options` is rejected for already-installed targets because changing integration options requires reinstalling managed files; run `upgrade <key> --integration-options ...` first, then `use <key>`.

## Use an Installed Integration

```bash
specify integration use <key>
```

| Option    | Description                                         |
| --------- | --------------------------------------------------- |
| `--force` | Overwrite managed shared templates while changing the default |

Sets the default integration without uninstalling any other installed integrations. This also refreshes managed shared templates so command references match the new default integration's invocation style. Modified or untracked shared templates are preserved unless `--force` is used.

## Upgrade an Integration

```bash
specify integration upgrade [<key>]
```

| Option                   | Description                                                              |
| ------------------------ | ------------------------------------------------------------------------ |
| `--force`                | Overwrite files even if they have been modified                          |
| `--script sh\|ps`        | Script type: `sh` (bash/zsh) or `ps` (PowerShell)                        |
| `--integration-options`  | Options for the integration                                              |

Reinstalls an installed integration with updated templates and commands (e.g., after upgrading Spec Kit). Defaults to the default integration; if a key is provided, it must be one of the installed integrations. Detects locally modified files and blocks the upgrade unless `--force` is used. Stale files from the previous install that are no longer needed are removed automatically. Shared templates stay aligned with the default integration even when upgrading a non-default integration.

## Integration-Specific Options

Some integrations accept additional options via `--integration-options`:

| Integration | Option              | Description                                                    |
| ----------- | ------------------- | -------------------------------------------------------------- |
| `generic`   | `--commands-dir`    | Required. Directory for command files                          |
| `kimi`      | `--migrate-legacy`  | Migrate legacy dotted skill directories to hyphenated format   |

Example:

```bash
specify integration install generic --integration-options="--commands-dir .myagent/cmds"
```

## FAQ

### Can I install multiple integrations in the same project?

Yes, but it is intended for team portability rather than the default workflow. Multiple integrations are allowed automatically only when the installed integration and the new integration are declared multi-install safe by Spec Kit. For other combinations, pass `--force` to acknowledge that multiple agents may see unrelated agent-specific instructions or commands.

Spec Kit tracks one default integration in `.specify/integration.json` with `default_integration`, all installed integrations with `installed_integrations`, per-integration runtime settings with `integration_settings`, and a dedicated `integration_state_schema` for future state migrations. The legacy `integration` field remains as an alias for the default integration.

### Which integrations are multi-install safe?

An integration is multi-install safe when it uses isolated agent directories, a dedicated context file that does not collide with another safe integration, stable command invocation settings, and a separate install manifest. Shared Spec Kit templates remain aligned to the single default integration.

The currently declared multi-install safe integrations are:

| Key | Isolation |
| --- | --------- |
| `auggie` | `.augment/commands`, `.augment/rules/specify-rules.md` |
| `claude` | `.claude/skills`, `CLAUDE.md` |
| `codebuddy` | `.codebuddy/commands`, `CODEBUDDY.md` |
| `codex` | `.agents/skills`, `AGENTS.md` |
| `cursor-agent` | `.cursor/skills`, `.cursor/rules/specify-rules.mdc` |
| `gemini` | `.gemini/commands`, `GEMINI.md` |
| `iflow` | `.iflow/commands`, `IFLOW.md` |
| `junie` | `.junie/commands`, `.junie/AGENTS.md` |
| `kilocode` | `.kilocode/workflows`, `.kilocode/rules/specify-rules.md` |
| `kimi` | `.kimi/skills`, `KIMI.md` |
| `qodercli` | `.qoder/commands`, `QODER.md` |
| `qwen` | `.qwen/commands`, `QWEN.md` |
| `roo` | `.roo/commands`, `.roo/rules/specify-rules.md` |
| `shai` | `.shai/commands`, `SHAI.md` |
| `tabnine` | `.tabnine/agent/commands`, `TABNINE.md` |
| `trae` | `.trae/skills`, `.trae/rules/project_rules.md` |
| `windsurf` | `.windsurf/workflows`, `.windsurf/rules/specify-rules.md` |

Integrations that share a context file or command directory with another integration, require dynamic install paths such as `--commands-dir`, or merge shared tool settings are not declared safe by default. They can still be installed alongside another integration with `--force`.

### What happens to my changes when I uninstall or switch?

Files you've modified are preserved automatically. Only unmodified files (matching their original SHA-256 hash) are removed. Use `--force` to override this.

### How do I know which key to use?

Run `specify integration list` to see all available integrations with their keys, or check the [Supported AI Coding Agents](#supported-ai-coding-agents) table above.

### Do I need the AI coding agent installed to use an integration?

CLI-based integrations (like Claude Code, Gemini CLI) require the tool to be installed. IDE-based integrations (like Windsurf, Cursor) work through the IDE itself. Some agents like GitHub Copilot support both IDE and CLI usage. `specify integration list` shows which type each integration is.

### When should I use `upgrade` vs `switch`?

Use `upgrade` when you've upgraded Spec Kit and want to refresh an installed integration's managed files. Use `switch` when you want to replace the current default with another integration; if the target is already installed, `switch` behaves like `use`.

