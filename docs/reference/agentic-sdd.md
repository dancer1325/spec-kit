# Agentic SDD -- `/speckit.*` -- 

* ⚠️requirements⚠️
  * [initialize SpecKit](../installation.md#how-to-initialize-github-speckit--project)

* agentic
  * == EACH command is run | your AI coding agent
  * [bug fix](agentic-bugfix.md)

* 💡types of invocation💡
  * 👀-- depend on -- your agent👀
    * `/speckit.*`
    * skills-based agents
      * `$speckit-*`
        * _Example:_ Codex, ZCode
      * `/skill:speckit-*` 
        * _Example:_ Kimi

* placed 
  * | ".<yourChosenAI>/commands/"
  * | ".<yourChosenAI>/prompts/"
  * if you use skills-based agents,
    * | ".<yourChosenAI>/skills/"

* recommendations
  * ⭐️[FULL step process](../quickstart.md)⭐️

    ```text
    /speckit.constitution -> /speckit.specify -> /speckit.clarify -> /speckit.plan -> /speckit.checklist -> /speckit.tasks -> /speckit.analyze -> /speckit.implement -> /speckit.converge
    ```
  * [E2E guide](../quickstart.md)

* are **context awareness**
  * == AUTOMATICALLY detect the active feature -- based on --  
    * ".specify/feature.json", OR 
      * if you want to replace it by anotherFile -> set `SPECIFY_FEATURE_DIRECTORY` environment variable
    * branchName
      * ⚠️requirements⚠️
        * install the Git extension
        * you have `git checkout -b anotherBranchRelatedToSpec` -> identify & update ".specify/feature.json" 
          * _Example:_ `001-feature-name`

## `/speckit.constitution <ARGUMENT>`

* responsible for
  * create OR update the [".specify/memory/constitution.md"](../concepts/sdd.md)
  * sync dependent templates
    * _Example:_ "CLAUDE.md", "GEMINI.md"
      * | kiro-cli, NOT exist
* 's arguments
  * project principles & guidelines
* uses
  * FIRST one
  * | change your principles

## `/speckit.specify <ARGUMENT>`

* responsible for
  * create OR updates the feature "specification" ("specs/") -- from a -- natural-language description
    * ⚠️if update == NEW feature -> create ANOTHER spec⚠️
* 's argument
  * what | user-facing perspective
    * == requirements & user stories
* ⚠️out of the scope
  * tech stack⚠️

## `/speckit.clarify <ARGUMENT>`

* == quality gate /
  * you can run >=1 time
* responsible for
  * asking your for <= 5 targeted questions -- about -- current spec's underspecified areas /
    * your answers are added | "specs/**/spec.md"
* 's arguments
  * focus area
    * allows: choose the spec 
    * OPTIONAL
      * == if you do NOT specify it -> chosen -- based on -- active spec
* use cases
  * BEFORE `/speckit.plan`
  * AFTER `/speckit.analyze`
    * ALTERNATIVE to
      * `/speckit.specify`

## `/speckit.plan <ARGUMENT>`

* responsible for
  * generate -- , from the spec, -- 
    * "specs/<feature>/plan.md" 
      * == implementation detail
    * "specs/<feature>/research.md"
* 's arguments
  * tech stack
  * architecture
  * technical constraints
* if AI coding agent gets stuck -> | AI assistant chat, `/speckit.analyze`

## `/speckit.checklist <ARGUMENT>`

* == quality checklist -- for -- the feature 
  * == checks 
    * whether the spec itself is: complete + clear + unambiguous + consistent
  * ⚠️if there are gaps ->
    * `/speckit.clarify` OR
    * `/speckit.specify`⚠️
* 's arguments
  * OPTIONAL
    * if NO passed -> broad pass

      ```text
      /speckit.checklist
      ```
    * if you specify it -> specify a focus area

      ```text
      /speckit.checklist Focus on the Kanban board interactions and comment permissions.
      ```

## `/speckit.tasks`

* generates -- , from the design artifacts, -- "specs/*/tasks.md" /
  * actionable
    * == -- for -- implementation
      * EVEN specifying the file path | implementation should happen
  * dependency-ordered
    * _Example:_ create the model, create the service, create the endpoint ...
  * priority-ordered (P1, P2,...)
  * `[P]`
    * == it can be executed in PARALLEL
  * organized into phases
    * setup
    * foundational
      * == block US
    * \>=1 user story
      * if you have specified TDD -> tests / user story 
    * polish
      * uses
        * cross-cutting concerns 
  * **Checkpoint validation / EACH user story phase**
  * if it's POSSIBLE -> parallel execution

## `/speckit.analyze`

* == consistent & quality analysis / 
  * read-only
    * ❌NEVER edits files❌
  * cross-artifact ("spec.md", "plan.md", "tasks.md")
  * report DIFFERENT categories: consistency + ambiguities + underspecification + coverage gaps + duplication + constitution
    * if there are issues
      * requirement problems -> run `/speckit.specify` OR `/speckit.clarify`
      * design problems -> run `/speckit.plan`
      * & you want to regenerate the task list -> run `/speckit.tasks`
    * if you have fixed ALL the issues -> `/speckit.analyze`
* use cases
  * BEFORE `/speckit.implement`
  * AFTER `/speckit.implement`
    * Reason:🧠extra review🧠

## `/speckit.implement`

* execute the tasks / specified | "tasks.md" /
  * respect 
    * dependency order
    * parallel markers
  * -- based on the -- feature
    * if it's small feature -> run it 1!

      ```text
      /speckit.implement
      ```

    * if it's a large feature -> run in task' phases

      ```bash
      /speckit.implement Implement only the Setup and Foundational phases: ...
      # /speckit.implement Implement only the Setup and Foundational phases: project scaffolding and the project/task data model with basic CRUD. Stop before the user-story features.
      ```

      ```bash
      /speckit.implement Now implement the ** user story: ...
      # /speckit.implement Now implement the Kanban board user story: drag-and-drop between columns.
      ```

* BEFORE moving to the next,
  * verify EACH stage works 

## `/speckit.converge`

* responsible for
  * assess the codebase vs feature's spec + plan + tasks
    * == confirm NOTHING was missed
* use cases
  * AFTER has run`/speckit.implement` | CURRENT "tasks.md"
* 's outcome
  * print a severity-graded findings summary
  * POSSIBLE ones
    * **Converged** 
      * == ❌NO find gaps❌
        * print: `✅ Converged — the implementation satisfies the spec, plan, and tasks.` 
      * "tasks.md" has NOT changed
      * NEXT steps
        * review OR open a PR
    * **Tasks appended** 
      * == find gaps
      * add NEW tasks | "tasks.md"'s convergence section  
        * ❌!= edit OR delete code❌
      * NEXT steps
        * `/speckit.implement` to complete them
        * `/speckit.converge` again
