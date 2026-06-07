# Presets

* Presets
  * == Spec Kit's collections of template + command /
    * stackable
    * priority-ordered  
  * let you
    * customize
      * artifacts / produced -- by the -- SSD workflow (specs, plans, tasks, checklists, constitutions)
      * commands / guide the LLM | creating them
        * WITHOUT forking OR modifying core files
  * discovered -- through -- [catalogs](#catalog-management)

## how does it work?

* [ARCHITECTURE](ARCHITECTURE.md)

## Command

* they are 
  * applied | install time
  * registered | ALL detected agent directories 
    * _Examples:_ ".claude/commands/", ".gemini/commands/", ... 
  * defined -- as -- `provides.templates.*` / `type: "command"`
    * == 💡template type💡
* | remove the preset,
  * the registered commands are cleaned up

## Script

* they are
  * defined -- as -- `provides.templates.*` / `type: "script"`
    * == 💡template type💡

## Quick Start

```bash
# Search AVAILABLE presets
specify preset search

# Install a preset -- from the -- catalog
specify preset add healthcare-compliance

# Install -- from a -- local directory
specify preset add --dev ./my-preset

# Install -- with a -- specific priority 
#   lower == HIGHER precedence
specify preset add healthcare-compliance --priority 5

# List INSTALLED presets
specify preset list

# TODO: See which template a name resolves to
specify preset resolve spec-template

# Get detailed info about a preset
specify preset info healthcare-compliance

# Remove a preset
specify preset remove healthcare-compliance
```

## Stacking Presets

* == 👀install SIMULTANEOUSLY >1 presets | SAME project👀
  * if you want to control which one wins -> pass `--priority` flag

    ```bash
    # base layer
    specify preset add enterprise-safe --priority 10
    
    # overrides enterprise-safe      
    specify preset add healthcare-compliance --priority 5  
    
    # overrides everything
    specify preset add pm-workflow --priority 1            
    ```

TODO: 
Presets **override by default**, they don't merge
* If two presets both provide `spec-template` with the default `replace` strategy, the one with the lowest priority number wins entirely
* However, presets can use **composition strategies** to augment rather than replace content.

### Composition Strategies

Presets can declare a `strategy` per template to control how content is combined
* The `name` field identifies which template to compose with in the priority stack, while `file` points to the actual content file (which can differ from the convention path `templates/<name>.md`):

```yaml
provides:
  templates:
    - type: "template"
      name: "spec-template"
      file: "templates/spec-addendum.md"
      strategy: "append"        # adds content after the core template
```

| Strategy            | Description                                                                                                             |
|---------------------|-------------------------------------------------------------------------------------------------------------------------|
| `replace` (default) | Fully replaces the lower-priority template                                                                              |
| `prepend`           | Places content **before** the resolved lower-priority template, separated by a blank line                               |
| `append`            | Places content **after** the resolved lower-priority template, separated by a blank line                                |
| `wrap`              | Content contains `{CORE_TEMPLATE}` placeholder (or `$CORE_SCRIPT` for scripts) replaced with the lower-priority content |

**Supported combinations:**

| Type | `replace` | `prepend` | `append` | `wrap` |
|------|-----------|-----------|----------|--------|
| **template** | ✓ (default) | ✓ | ✓ | ✓ |
| **command** | ✓ (default) | ✓ | ✓ | ✓ |
| **script** | ✓ (default) | — | — | ✓ |

Multiple composing presets chain recursively
* For example, a security preset with `prepend` and a compliance preset with `append` will produce:
security header + core content + compliance footer.

## Catalog Management

* Spec Kit
  * by default, uses
    * [official catalog](catalog.json)
    * [community catalog](catalog.community.json)

```bash
# List active catalogs
specify preset catalog list

# Add a custom catalog
specify preset catalog add https://example.com/catalog.json --name my-org --install-allowed

# Remove a catalog
specify preset catalog remove my-org
```

### [built-in catalog](catalog.json)

### [Community Catalog](catalog.community.json)

* INDEPENDENT -- to -- built-in
* customize how Spec Kit behaves
  * == override -- WITHOUT -- changing any tooling
    * templates
    * commands
    * terminology 

## how to create a preset?

* _Example:_ [here](scaffold/)

## Environment Variables

| Variable                     | Description                                                                                                                                                                                                                                                                                                                                                                                       | Default                |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| `SPECKIT_PRESET_CATALOG_URL` | override the FULL catalog stack -- with -- 1! URL (replaces ALL defaults)                                                                                                                                                                                                                                                                                                                         | Built-in default stack |
| `GH_TOKEN` / `GITHUB_TOKEN`  | GitHub token / <br/> &nbsp;&nbsp; authenticate requests -- to -- GitHub-hosted URLs (`raw.githubusercontent.com`, `github.com`, `api.github.com`, `codeload.github.com`) <br/> &nbsp;&nbsp; is attached AUTOMATICALLY \| requests / target GitHub domains <br/> use cases: your catalog JSON OR preset ZIPs are hosted \| private GitHub repository <br/> NOT use cases: NON-GitHub catalog URLs  | None                   |

## Configuration Files

| File                             | Scope   | Description                         |
|----------------------------------|---------|-------------------------------------|
| `.specify/preset-catalogs.yml`   | Project | project's custom catalog stack      |
| `~/.specify/preset-catalogs.yml` | User    | ALL projects' custom catalog stack  |

## Future considerations | future releases

* **Structural merge strategies** 
  * == parse Markdown sections / section granularity
    * _Example:_ "replace only ## Security"
* **Conflict detection** 
  * `specify preset lint` / `specify preset doctor`

## [how to build & publish your OWN preset?](PUBLISHING.md)
