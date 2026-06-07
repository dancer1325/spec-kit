# Presets
## == Spec Kit's collections of template + command
TODO:
### stackable
TODO:
### priority-ordered
TODO:
## let you customize
### artifacts / produced -- by the -- SSD workflow (specs, plans, tasks, checklists, constitutions)
TODO:
### commands / guide the LLM | creating them
TODO:
#### WITHOUT forking OR modifying core files
TODO:

# Environment Variables
## `SPECKIT_PRESET_CATALOG_URL`
TODO:
## `GH_TOKEN` / `GITHUB_TOKEN`
### -- by -- using a private GitHub-hosted catalog

```bash
# Authenticate -- with a -- token (gh CLI, PAT, or GITHUB_TOKEN in CI)
export GITHUB_TOKEN=$(gh auth token)

# Search a private catalog / added -- via -- `specify preset catalog add`
specify preset search my-template

# Install -- from a -- private catalog
specify preset add my-template
```
