# Quick Start Guide

## 6-Step Process

* **Context Awareness**
  * Spec Kit commands 
    * placed | .yourChosenAI/commands/
    * AUTOMATICALLY detect the active feature -- based on -- your current Git branch (e.g., `001-feature-name`)
      * if you want to switch BETWEEN DIFFERENT specifications -> switch Git branches

* [SDD](../spec-driven.md)

### install Specify CLI

#### Option 1: Persistent Installation
* 👀recommended👀

* steps
  * install [uv](https://docs.astral.sh/uv/getting-started/installation/)
    * `curl -LsSf https://astral.sh/uv/install.sh | sh`
    * `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc`
  * `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git`
  * `specify version`
    * check that it's installed
  * [initialize the project](installation.md#initialize-a-new-project)
  * `specify check`
    * check the installed tools

* pros
  - Tool stays installed & available | PATH
  - NO need to create shell aliases
  - Better tool management: `uv tool list`, `uv tool upgrade`, `uv tool uninstall`
  - Cleaner shell configuration

#### Option 2: 1-time Usage

* steps
  * `uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>`

### establish project principles

* steps
  * | your project directory,
    * launch your AI assistant 
  * | AI assistant,
    * `/speckit.constitution WriteCommandToCreateYourProject'sGoverningPrinciplesAndDevelopmentGuidelines`
      * modify .specify/memory/constitution.md

### create the spec

* | claude chat
  * `/speckit.specify describeWhatAndWhyToBuild`
    * ❌NO specify the tech stack❌
    * check that it 
      * created "specs/"
      * branched

### refine the spec

* | claude chat
  * `/speckit.clarify WriteToIdentifyAndResolveAmbiguitiesInYourSpecification`
    * check that it 
      * creates specs/*/spec.md

### create a technical implementation plan

* | claude chat
  * `/speckit.plan provideYourTechStackAndArchiteChoices`
    * check that it 
      * creates specs/*/plan.md

### break down into tasks

* | claude chat
  * `/speckit.tasks` 
    * FROM your implementation plan, create an actionable task list 
    * create specs/*/tasks.md

### validate the plan

* OPTIONAL
* | claude chat
  * `/speckit.analyze`
    * if there are something to improve -> pass yes -- as -- input

### execute implementation

* | claude chat
  * `/speckit.implement`
    * execute ALL tasks
    * build your feature -- based on the -- plan

## Key Principles

* TODO: 
- **Be explicit** about what you're building and why
- **Don't focus on tech stack** during specification phase
- **Iterate and refine** your specifications before implementation
- **Validate** the plan before coding begins
- **Let the AI agent handle** the implementation details

## Notes

- _Examples:_
  - [of Spec's steps](../templates)
  - [firstProject](https://github.com/dancer1325/spec-kit-firstExample)
  - [secondProject](https://github.com/dancer1325/spec-kit-secondExample)
