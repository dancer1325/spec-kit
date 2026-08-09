# Spec Kit Extensions

* == modular packages / 
  * add NEW commands & functionality | Spec Kit
    * ⚠️WITHOUT modifying the core framework⚠️
  * are discovered -- through -- catalogs /
    * [have priority](EXTENSION-USER-GUIDE.md)
  * allows you to
    * integrate -- with -- EXTERNAL tools
      * _Examples:_ Jira, Linear, GitHub, etc.
    * AUTOMATE repetitive tasks -- via -- hooks
    * customize workflows
    * share solutions ACROSS projects
  * | 1 project,
    * there can be > 1 extension
  * community driven 
    * == anyone can create & share extensions
  * versioned INDEPENDENTLY

## Extension Catalogs

### [built-in catalog](catalog.json) 

* == default catalog of extensions /
  * by default, 
    * empty 
  * `specify extension <COMMAND>` use it
* `SPECKIT_CATALOG_URL`
  * == environment variable /
    * override the upstream default
  * steps to make it effective

    ```bash
    # 1. override the default upstream catalog -- with -- your organization's catalog
    export SPECKIT_CATALOG_URL="https://your-org.com/spec-kit/catalog.json"
    
    # 2. NOW, it uses your organization's catalog
    specify extension search
    ```

* TODO: ways to customize
  * | community catalog, copy entries -- into -- your org catalog, OR
  * add DIRECTLY your OWN extensions

### [Community Catalog](catalog.community.json)

* Community extensions
  * INDEPENDENTLY created & maintained -- by -- their respective authors
    * == maintainers
      * ONLY verify that catalog entries are complete & correctly formatted
      * do NOT review, audit, endorse, or support the extension code
    * -> use under your risks
  * published | https://speckit-community.github.io/extensions/
  * [how to submit](#submission-process)

## how to make extensions AVAILABLE?

* [MORE detailed](EXTENSION-USER-GUIDE.md)

### Option 1: Curated Catalog

* allows
  * FULL control about the AVAILABLE extensions
* use case
  * Organizations

* goal
  * populate your "catalog.json" -- with -- approved extensions

* steps
  1. FROM >1 sources, discover extensions
  2. review extensions & choose them
  3. add those | your OWN "catalog.json"
     * -> team members can NOW
       * `specify extension search`
         * == find them
       * `specify extension add <name>`
         * install them

### Option 2: DIRECT URLs 

* use case
  * test the extension WITHOUT install it
    * == ❌NO installed | catalog❌
    * -> ❌NOT found -- via -- `specify extension search`❌
* allows
  * team members can DIRECTLY install them

```bash
specify extension add <extension-name> --from https://github.com/org/spec-kit-ext/archive/refs/tags/v1.0.0.zip
```

## how to add your extension?

### Submission Process

* [here](EXTENSION-PUBLISHING-GUIDE.md)

### Submission Checklist

* [here](EXTENSION-PUBLISHING-GUIDE.md)

## `category`

* included ALSO | `extension.<EXTENSION_NAME>.tags`
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

## `effect`

* AVAILABLE ones
  * `Read-only` 
    * produces reports WITHOUT modifying files
  * `Read+Write`
    * modifies files, creates artifacts, or updates specs
