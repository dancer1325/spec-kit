# Spec Kit Extensions

* goal
  * add NEW functionality 
    * ⚠️WITHOUT bloating the core framework⚠️

## Extension Catalogs

### [built-in catalog](catalog.json) 

* == default catalog of extensions /
  * by default, empty 
  * `specify extension <COMMAND>` use it

* TODO: 
- **Org Catalog**: Point `SPECKIT_CATALOG_URL` at your organization's fork or hosted catalog JSON to use it instead of the upstream default
- **Customization**: Copy entries from the community catalog into your org catalog, or add your own extensions directly

**Example override:**
```bash
# Override the default upstream catalog with your organization's catalog
export SPECKIT_CATALOG_URL="https://your-org.com/spec-kit/catalog.json"
specify extension search  # Now uses your organization's catalog instead of the upstream default
```

### [Community Catalog](catalog.community.json)

> [!NOTE]
> Community extensions are independently created and maintained by their respective authors
> Maintainers only verify that catalog entries are complete and correctly formatted — they do **not review, audit, endorse, or support the extension code itself**
> Review extension source code before installation and use at your own discretion.

- **Purpose**: Browse available community-contributed extensions
- **Status**: Active - contains extensions submitted by the community
- **Location**: `extensions/catalog.community.json`
- **Usage**: Reference catalog for discovering available extensions
- **Submission**: Open to community contributions via [issue template](https://github.com/github/spec-kit/issues/new?template=extension_submission.yml)

**How It Works:**

## Making Extensions Available

You control which extensions your team can discover and install:

### Option 1: Curated Catalog (Recommended for Organizations)

Populate your `catalog.json` with approved extensions:

1. **Discover** extensions from various sources:
   - Browse `catalog.community.json` for community extensions
   - Find private/internal extensions in your organization's repos
   - Discover extensions from trusted third parties
2. **Review** extensions and choose which ones you want to make available
3. **Add** those extension entries to your own `catalog.json`
4. **Team members** can now discover and install them:
   - `specify extension search` shows your curated catalog
   - `specify extension add <name>` installs from your catalog

**Benefits**: Full control over available extensions, team consistency, organizational approval workflow

**Example**: Copy an entry from `catalog.community.json` to your `catalog.json`, then your team can discover and install it by name.

### Option 2: Direct URLs (For Ad-hoc Use)

Skip catalog curation - team members install directly using URLs:

```bash
specify extension add <extension-name> --from https://github.com/org/spec-kit-ext/archive/refs/tags/v1.0.0.zip
```

**Benefits**: Quick for one-off testing or private extensions

**Tradeoff**: Extensions installed this way won't appear in `specify extension search` for other team members unless you also add them to your `catalog.json`.

## Available Community Extensions

> [!NOTE]
> Community extensions are independently created and maintained by their respective authors. Maintainers only verify that catalog entries are complete and correctly formatted — they do **not review, audit, endorse, or support the extension code itself**. The Community Extensions website is also a third-party resource. Review extension source code before installation and use at your own discretion.

🔍 **Browse and search community extensions on the [Community Extensions website](https://speckit-community.github.io/extensions/).**

See the [Community Extensions](https://github.github.io/spec-kit/community/extensions.html) page for the full list of available community-contributed extensions.

For the raw catalog data, see [`catalog.community.json`](catalog.community.json).


## Adding Your Extension

### Submission Process

To add your extension to the community catalog:

1. **Prepare your extension** following the [Extension Development Guide](EXTENSION-DEVELOPMENT-GUIDE.md)
2. **Create a GitHub release** for your extension
3. **File an issue** using the [Extension Submission](https://github.com/github/spec-kit/issues/new?template=extension_submission.yml) template with all required metadata
4. **Wait for review** — a maintainer will review the submission, update the catalog, and close the issue

See the [Extension Publishing Guide](EXTENSION-PUBLISHING-GUIDE.md) for detailed step-by-step instructions.

### Submission Checklist

Before submitting, ensure:

- ✅ Valid `extension.yml` manifest
- ✅ Complete README with installation and usage instructions
- ✅ LICENSE file included
- ✅ GitHub release created with semantic version (e.g., v1.0.0)
- ✅ Extension tested on a real project
- ✅ All commands working as documented

## how to install extensions?

* requirements
  * `specify init`
    * == Specify project / ALREADY initialized

```bash
specify extension add <name> [OPTION]
# 1. -- from -- URL

# 2. -- from -- URL
# specify extension add <extension-name> --from https://github.com/<org>/<repo>/archive/refs/tags/<version>.zip
```

| Option          | Description                                                               |
| --------------- |---------------------------------------------------------------------------|
| `--dev`         | Install -- from a -- local directory <br/> use cases: development         |
| `--from <url>`  | Install -- from a -- custom URL (!= catalog)                              |
| `--priority <N>`| Resolution priority <br/> by default, 10 <br/> lower == HIGHER precedence |

* [MORE](EXTENSION-USER-GUIDE.md)

* Extension commands are automatically registered with the currently installed AI coding agent integration.

# how to remove an Extension?

```bash
specify extension remove <name> [OPTION]
```

| Option          | Description                                    |
| --------------- | ---------------------------------------------- |
| `--keep-config` | Preserve configuration files during removal    |
| `--force`       | Skip confirmation prompt                       |

Configuration files are backed up by default; use `--keep-config` to leave them in place or `--force` to skip the confirmation.

# Categories

* included | `extension.<EXTENSION_NAME>.tags`
* AVAILABLE ones
  * `docs` 
    * reads, validates, or generates spec artifacts
  * `code`
    * reviews, validates, or modifies source code
  * `process`
    * orchestrates workflow across phases
  * `integration` 
    * syncs with external platforms
  * `visibility`
    * reports on project health or progress

# Effect

* AVAILABLE ones
  * `Read-only` 
    * produces reports without modifying files
  * `Read+Write`
    * modifies files, creates artifacts, or updates specs

Extensions add new capabilities to Spec Kit
domain-specific commands, external tool integrations, quality gates, and more
They introduce new commands and templates that go beyond the built-in Spec-Driven Development workflow.

Extensions add new capabilities to Spec Kit — domain-specific commands, external tool integrations, quality gates, and more
* They are discovered through catalogs and can be installed, updated, enabled, disabled, or removed independently
* Multiple extensions can coexist in a single project.

# Search Available Extensions

```bash
specify extension search [query]
```

| Option       | Description                          |
| ------------ | ------------------------------------ |
| `--tag`      | Filter by tag                        |
| `--author`   | Filter by author                     |
| `--verified` | Show only verified extensions        |

Searches all active catalogs for extensions matching the query. Without a query, lists all available extensions.

# List Installed Extensions

```bash
specify extension list
```

| Option        | Description                                        |
| ------------- | -------------------------------------------------- |
| `--available` | Show available (uninstalled) extensions            |
| `--all`       | Show both installed and available extensions       |

Lists installed extensions with their status, version, and command counts.

# Extension Info

```bash
specify extension info <name>
```

Shows detailed information about an installed or available extension, including its description, version, commands, and configuration.

# Update Extensions

```bash
specify extension update [<name>]
```

Updates a specific extension, or all installed extensions if no name is given.

# Enable / Disable an Extension

```bash
specify extension enable <name>
specify extension disable <name>
```

Disable an extension without removing it. Disabled extensions are not loaded and their commands are not available. Re-enable with `enable`.

# Set Extension Priority

```bash
specify extension set-priority <name> <priority>
```

Changes the resolution priority of an extension. When multiple extensions provide a command with the same name, the extension with the lowest priority number takes precedence.

## Catalog Management

Extension catalogs control where `search` and `add` look for extensions. Catalogs are checked in priority order (lower number = higher precedence).

## List Catalogs

```bash
specify extension catalog list
```

Shows all active catalogs in the stack with their priorities and install permissions.

## Add a Catalog

```bash
specify extension catalog add <url>
```

| Option                               | Description                                        |
| ------------------------------------ | -------------------------------------------------- |
| `--name <name>`                      | Required. Unique name for the catalog              |
| `--priority <N>`                     | Priority (default: 10; lower = higher precedence)  |
| `--install-allowed / --no-install-allowed` | Whether extensions can be installed from this catalog |
| `--description <text>`               | Optional description                               |

Adds a catalog to the project's `.specify/extension-catalogs.yml`.

## Remove a Catalog

```bash
specify extension catalog remove <name>
```

Removes a catalog from the project configuration.

## Catalog Resolution Order

Catalogs are resolved in this order (first match wins):

1. **Environment variable** — `SPECKIT_CATALOG_URL` overrides all catalogs
2. **Project config** — `.specify/extension-catalogs.yml`
3. **User config** — `~/.specify/extension-catalogs.yml`
4. **Built-in defaults** — official catalog + community catalog

Example `.specify/extension-catalogs.yml`:

```yaml
catalogs:
  - name: "my-org-catalog"
    url: "https://example.com/catalog.json"
    priority: 5
    install_allowed: true
    description: "Our approved extensions"
```

# Extension Configuration

Most extensions include configuration files in their install directory:

```text
.specify/extensions/<ext>/
├── <ext>-config.yml           # Project config (version controlled)
├── <ext>-config.local.yml     # Local overrides (gitignored)
└── <ext>-config.template.yml  # Template reference
```

Configuration is merged in this order (highest priority last):

1. **Extension defaults** (from `extension.yml`)
2. **Project config** (`<ext>-config.yml`)
3. **Local overrides** (`<ext>-config.local.yml`)
4. **Environment variables** (`SPECKIT_<EXT>_*`)

To set up configuration for a newly installed extension, copy the template:

```bash
cp .specify/extensions/<ext>/<ext>-config.template.yml \
   .specify/extensions/<ext>/<ext>-config.yml
```

# FAQ

## Why can't I find an extension with `search`?

Check the spelling of the extension name. The extension may not be published yet, or it may be in a catalog you haven't added. Use `specify extension catalog list` to see which catalogs are active.

## Why doesn't the extension command appear in my AI coding agent?

Verify the extension is installed and enabled with `specify extension list`. If it shows as installed, restart your AI coding agent — it may need to reload for it to take effect.

## How do I set up extension configuration?

Copy the config template that ships with the extension:

```bash
cp .specify/extensions/<ext>/<ext>-config.template.yml \
   .specify/extensions/<ext>/<ext>-config.yml
```

See [Extension Configuration](#extension-configuration) for details on config layers and overrides.

## How do I resolve an incompatible version error?

Update Spec Kit to the version required by the extension.

## Who maintains extensions?

Most extensions are independently created and maintained by their respective authors. The Spec Kit maintainers do not review, audit, endorse, or support extension code. Review an extension's source code before installing and use at your own discretion. For issues with a specific extension, contact its author or file an issue on the extension's repository.
