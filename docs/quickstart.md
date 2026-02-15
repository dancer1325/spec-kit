# Quick Start Guide

## 7-Step Process

* **Context Awareness**
  * Spec Kit commands 
    * placed | .yourChosenAI/commands/
    * AUTOMATICALLY detect the active feature -- based on -- your current Git branch (e.g., `001-feature-name`)
      * if you want to switch BETWEEN DIFFERENT specifications -> switch Git branches

* ⭐️'s key principles⭐️
  - **Be explicit** -- about -- WHAT you're building & why
  - | specification phase, 
    - **NOT focus on tech stack** 
  - BEFORE implementation,
    - **Iterate & refine** your specifications 
    - **Validate** the plan
  - **Let the AI agent handle** the implementation details
  - [SDD](../spec-driven.md)

### 0. install Specify CLI

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
    * follow [initialize the project](installation.md#initialize-a-new-project)

### 1. establish project principles

* steps
  * | your project directory,
    * launch your AI assistant 
  * | AI assistant chat,
    * `/speckit.`
      * ALL [/commands](cli.md#speckit----slash-commands---) are available
    * `/speckit.constitution WriteCommandToCreateYourProject'sGoverningPrinciplesAndDevelopmentGuidelines`
      * modify .specify/memory/constitution.md
      * goal
        * ensure consistent decision-making | ALL subsequent development phases

* .specify/memory/constitution.md
  * uses
    * by AI agent | specification, planning, and implementation phases

### 2. create the spec

* | AI assistant chat
  * `/speckit.specify describeExplicitlyWhatAndWhyToBuild`
    * ❌NO specify the tech stack❌
    * check that it 
      * created "specs/"
        * US & functional requirements
      * branched

### 3. refine the spec

* | AI assistant chat
  * `/speckit.clarify WriteToIdentifyAndResolveAmbiguitiesInYourSpecification`
    * check that it 
      * creates specs/*/spec.md

### 4. create a technical implementation plan

* | AI assistant chat
  * `/speckit.plan provideYourTechStackAndArchiteChoices`
    * check that it 
      * creates 
        * specs/*/plan.md
        * specs/*/research.md
    * if Claude Code gets stuck -> ask it to clarify

### 5. break down into tasks

* | AI assistant chat
  * `/speckit.tasks` 
    * FROM your implementation plan, create an actionable task list 
    * create specs/*/tasks.md
      - **Task breakdown -- by -- user story** 
        - separate implementation phase (+ its own set of tasks) / EACH user story
      - **Dependency management BETWEEN components**
        - _Examples:_ 
          - models BEFORE services
          - services BEFORE endpoints
      - **Parallel execution markers** `[P]`
        - optimize development workflow
      - **File path specifications | implementation should occur**
      - **Test-driven development structure**
        - == test BEFORE implementation
      - **Checkpoint validation / EACH user story phase**

### 6. validate the plan

* OPTIONAL
* | AI assistant chat
  * `/speckit.analyze`
    * if there are something to improve -> pass yes -- as -- input

* recommendations
  * | your current branch, create a PR to "main"

### 7. execute implementation

* | AI assistant chat
  * `/speckit.implement`
    * execute ALL tasks / 
      * specified | specs/*/tasks.md
      * respect dependency order
    * build your feature 
      * -- based on the -- plan
      * follow TDD

## Notes

- _Examples:_
  - [of Spec's steps](../templates)
  - [firstProject](https://github.com/dancer1325/spec-kit-firstExample)
  - [secondProject](https://github.com/dancer1325/spec-kit-secondExample)
