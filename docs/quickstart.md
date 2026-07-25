# Quick Start Guide

* **Context Awareness**
  * TODO: Spec Kit commands 
    * placed | .yourChosenAI/commands/
    * AUTOMATICALLY detect the active feature -- based on -- your current Git branch (e.g., `001-feature-name`)
      * if you want to switch BETWEEN DIFFERENT specifications -> switch Git branches
      * TODO: unless you pass `--script sh|ps`
  * TODO: 
    * Spec Kit tracks the active feature by the feature directory recorded in `.specify/feature.json` (overridable with the `SPECIFY_FEATURE_DIRECTORY` environment variable)
    * Commands resolve the feature from that state, **not** from the checked-out Git branch — no Git required
    * The opt-in **git** extension adds numbered feature branches (e.g. `001-feature-name`) for organizing work in version control, 
    but the active feature is still whichever directory that state points to; `git checkout` alone does not change it
    * To point commands at a different feature, update `.specify/feature.json` (or set `SPECIFY_FEATURE_DIRECTORY`).

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

### 1. establish project principles -- `/speckit.constitution` --

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

TODO:
Establishes the project's guiding principles, which every later step is evaluated against. Run it once up front, passing your principles as arguments.

_Example:_

```text
/speckit.constitution Taskify is a "Security-First" application. All user inputs must be validated. We use a microservices architecture. Code must be fully documented.
```

### 2. `/speckit.specify` -- describe what to build --

* | AI assistant chat
  * `/speckit.specify describeExplicitlyWhatAndWhyToBuild`
    * ❌NO specify the tech stack❌
    * check that it 
      * created "specs/"
        * US & functional requirements
      * branched

TODO:
Creates the feature specification from a natural-language description. Focus on the **what** and **why**, not the tech stack.

_Example:_ 
```text
/speckit.specify Develop Taskify, a team productivity platform where predefined users create projects, assign tasks, comment, and move tasks across Kanban columns (To Do, In Progress, In Review, Done). Five users (one product manager, four engineers), three sample projects, no login for this first phase.
```

### 3. `/speckit.clarify` — resolve ambiguities

* | AI assistant chat
  * `/speckit.clarify WriteToIdentifyAndResolveAmbiguitiesInYourSpecification`
    * check that it 
      * creates specs/*/spec.md

TODO: Asks targeted questions about anything underspecified and folds your answers back into the spec, so you're not planning on top of ambiguity. Run it before planning, optionally with a focus area.

```text
/speckit.clarify Focus on task card behavior — status changes, comment permissions, and user assignment.
```


### 4. `/speckit.plan` — choose the tech stack

* | AI assistant chat
  * `/speckit.plan provideYourTechStackAndArchiteChoices`
    * check that it 
      * creates 
        * specs/*/plan.md
        * specs/*/research.md
    * if Claude Code gets stuck -> ask it to clarify

* OPTIONAL
* | AI assistant chat
  * `/speckit.analyze`
    * if there are something to improve -> pass yes -- as -- input

* recommendations
  * | your current branch, create a PR to "main"

TODO:

Generates the design artifacts from the spec. This is where implementation detail belongs — provide your tech stack and architecture.

```text
/speckit.plan Use .NET Aspire with Postgres. The frontend is Blazor Server with drag-and-drop boards and real-time updates. Expose REST APIs for projects, tasks, and notifications.
```

### Step 5: `/speckit.checklist` — validate the spec

TODO: 
Generates a quality checklist — "unit tests for your requirements" — to confirm the spec is complete, clear, and consistent before you break the work down.

```text
/speckit.checklist
```

### 6. `/speckit.tasks` -- break down into tasks

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

TODO:
Generates an actionable, dependency-ordered `tasks.md` from the design artifacts.

```text
/speckit.tasks
```

### Step 7: `/speckit.analyze` -- check consistency --

TODO:
Reports conflicts, gaps, and ambiguities across `spec.md`, `plan.md`, and `tasks.md`. It's read-only — if it flags issues, fix them at the source and re-run before implementing.

```text
/speckit.analyze
```

### 8. `/speckit.implement` -- execute implementation --

* | AI assistant chat
  * `/speckit.implement`
    * execute ALL tasks / 
      * specified | specs/*/tasks.md
      * respect dependency order
    * build your feature 
      * -- based on the -- plan
      * follow TDD

TODO:
Executes the tasks in `tasks.md` in dependency order. Run it once to build everything, or scope it to one phase at a time for large features.

### Step 9: `/speckit.converge` — verify completeness

Checks the codebase against the spec, plan, and tasks. If it finds gaps, it appends new tasks to `tasks.md`; run `/speckit.implement` and converge again until it reports converged. Otherwise you're done — proceed to review or open a PR.

## Notes

* [complete methodology](../spec-driven.md)
* _Examples:_
  * [of Spec's steps](../templates)
  * [firstProject](https://github.com/dancer1325/spec-kit-firstExample)
  * [secondProject](https://github.com/dancer1325/spec-kit-secondExample)
