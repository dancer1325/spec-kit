# Quick Start Guide

* **Context Awareness**
  * TODO: Spec Kit commands 
    * placed | .yourChosenAI/commands/
    * AUTOMATICALLY detect the active feature -- based on -- your current Git branch (e.g., `001-feature-name`)
      * if you want to switch BETWEEN DIFFERENT specifications -> switch Git branches
      * TODO: unless you pass `--script sh|ps`

* ⭐️'s key principles⭐️
  - **Be explicit** -- about -- WHAT you're building & why
  - | specification phase, 
    - **NOT focus on tech stack** 
  - BEFORE implementation,
    - **Iterate & refine** your specifications 
    - **Validate** the plan
  - **Let the AI agent handle** the implementation details
  - [SDD](../spec-driven.md)

* ⭐️types of paths⭐️
  * 💡short💡
    * step process
      * install Specify CLI
      * `/speckit.specify`
      * `/speckit.plan`
      * `/speckit.tasks`
      * `/speckit.implement`
      * `/speckit.converge`
    * use case
      * small features
  * 💡full💡 
    * step process
      * install Specify CLI
      * `/speckit.constitution`
      * `/speckit.specify`
      * `/speckit.clarify`
      * `/speckit.plan`
      * `/speckit.checklist`
      * `/speckit.tasks`
      * `/speckit.analyze`
      * `/speckit.implement`
      * `/speckit.converge`
    * use case
      * production features

## Step Processes

### 0. install Specify CLI

* steps
  * [install prerequirements + Github speckit](installation.md#how-to-install)
  * [initialize Github Speckit](installation.md#how-to-initialize-github-speckit--project)

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

* [complete methodology](../spec-driven.md)
* _Examples:_
  * [of Spec's steps](../templates)
  * [firstProject](https://github.com/dancer1325/spec-kit-firstExample)
  * [secondProject](https://github.com/dancer1325/spec-kit-secondExample)
