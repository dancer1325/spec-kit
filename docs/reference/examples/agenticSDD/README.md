# Agentic SDD -- `/speckit.*` --
## requirements: initialize SpecKit
* [here](example)
  * `specify init .`
## agentic == EACH command is run | your AI coding agent
* check NEXT sections
## types of invocation -- depend on -- your agent
### `/speckit.*` → placed | `.<agent>/commands/` OR `.<agent>/prompts/`
* [here](example/.kiro/prompts)
### skills-based agents → placed | `.<agent>/skills/speckit-<name>/SKILL.md`
TODO:
#### `$speckit-*` (Codex, ZCode)
TODO:
#### `/skill:speckit-*` (Kimi)
TODO:
## recommendations: FULL step process
* [here](../../../examples/quickstart)
## are Context Awareness
### == AUTOMATICALLY detect the active feature -- based on --
#### ".specify/feature.json", OR
TODO:
##### if you want to replace it by anotherFile -> set `SPECIFY_FEATURE_DIRECTORY` environment variable
TODO:
#### branchName
* follow the requirements
TODO:

# `/speckit.constitution`
* | [here](example)
  * `kiro-cli`
    * `/speckit.constitution This project follows a "Library-First" approach. All features must be implemented as standalone libraries first. We use TDD strictly. We prefer functional programming patterns.`
## responsible for
### create OR update project governing principles & development guidelines
* [here](example/.specify/memory/constitution.md)
### sync dependent templates
TODO: 
## 's arguments: project principles & guidelines
* `/speckit.constitution This project follows a "Library-First" approach. All features must be implemented as standalone libraries first. We use TDD strictly. We prefer functional programming patterns.`
## uses
### FIRST one
* [here](example)
### | change your principles
* `/speckit.constitution TDD is NOT needed, just optional.`
  * check ".specify/memory/constitution.md" NOT contain TDD as mandatory

# `/speckit.specify`
* | [here](example)
  * `kiro-cli`
    * `/speckit.specify Build an application that helps me organize photos into albums grouped by date, re-orderable by drag-and-drop on the main page, with a tile preview inside each album.`
      * check it generates [specs/](example/specs)
## responsible for: 
### create the feature "specification" -- from a -- natural-language description
* check the input
### update the feature "specification" -- from a -- natural-language description
* `/speckit.specify Update: the drag-and-drop reordering should also work within individual albums,
  not just on the main page.`
  * check [specs001](example/specs/001-photo-album-organizer) was modified
#### ⚠️if update == NEW feature -> create ANOTHER spec⚠️
* `/speckit.specify Add a sharing feature: users can share individual albums or specific photos via
  a link. Shared links expire after 7 days and can be revoked by the owner.`
## 's input: what | user-facing perspective == requirements & user stories
* check the input
## ❌ NOT focus on tech stack ❌
* check the input
## out of the scope: tech stack
* check the input

# `/speckit.clarify`
* | [here](example)
  * `kiro-cli`
    * `/speckit.clarify Focus on the task card behavior: status changes, comment limits, and who can be assigned.`
## == quality gate
* check the questions suggested -- to -- review 
### / you can run >=1 time
* | [here](example)
  * `kiro-cli`
    * `/speckit.clarify`
## responsible for: asking <= 5 targeted questions -- about -- current spec's underspecified areas
* check the questions suggested -- to -- review
### your answers are added | "specs/**/spec.md"
* check the answers are added | "specs/**/spec.md"
## 's arguments: focus area (OPTIONAL)
* | [here](example)
  * `kiro-cli`
    * `/speckit.clarify`
### == if you do NOT specify it -> chosen -- based on -- active spec
* check the AI coding agent lines
## use cases
### BEFORE `/speckit.plan`
* [here](example)
### AFTER `/speckit.analyze` -- ALTERNATIVE to -- `/speckit.specify`
TODO:

# `/speckit.plan`
* | [here](example)
  * `kiro-cli`
    * `/speckit.plan Use .NET Aspire with Postgres. The frontend is Blazor Server with drag-and-drop boards and real-time updates. Expose REST APIs for projects, tasks, and notifications.`
## responsible for: generate -- , from the spec, -- 
### "specs/<feature>/plan.md"
* [here](example/specs/001-photo-album-organizer/plan.md)
### "specs/<feature>/research.md"
* [here](example/specs/001-photo-album-organizer/research.md)
## 's arguments: tech stack + architecture + technical constraints as arguments
* check the input

# `/speckit.checklist`
* | [here](example)
  * `kiro-cli`
    * `/speckit.checklist`
## == quality (complete + clear + unambiguous + consistent) checklist -- for -- the feature
* [requirements.md](example/specs/002-album-photo-sharing/checklists/requirements.md)
* [review.md](example/specs/002-album-photo-sharing/checklists/review.md)
### ⚠️ if it surfaces gaps →
#### `/speckit.clarify` 
* check how we run -- for -- MAIN focus area
  * `/speckit.clarify Security/Privacy`
#### OR `/speckit.specify`
TODO:
## 's arguments
### `/speckit.checklist`
* check previous input
### `/speckit.checklist ....`
TODO:

# `/speckit.tasks`
* | [here](example)
  * `kiro-cli`
    * `/speckit.tasks`
## generates -- from the design artifacts -- a `tasks.md`
* [spec-001](example/specs/002-album-photo-sharing/tasks.md)
* [spec-002](example/specs/002-album-photo-sharing/tasks.md)
### actionable == -- for -- implementation
TODO:
#### EVEN specifying the file path | implementation should happen
TODO:
### dependency-ordered
* tasks have an order
  * [spec-001](example/specs/002-album-photo-sharing/tasks.md)
  * [spec-002](example/specs/002-album-photo-sharing/tasks.md) 
### priority-ordered (P1, P2,...)
* see P1, P2, P3 ... |
  * [spec-001](example/specs/002-album-photo-sharing/tasks.md)
  * [spec-002](example/specs/002-album-photo-sharing/tasks.md) 
### `[P]` == it can be executed in PARALLEL
* [spec-001](example/specs/002-album-photo-sharing/tasks.md)
* [spec-002](example/specs/002-album-photo-sharing/tasks.md)
### organized into phases
* [spec-001](example/specs/002-album-photo-sharing/tasks.md)
* [spec-002](example/specs/002-album-photo-sharing/tasks.md)
#### 1. Setup
TODO:
#### 2. Foundational
TODO:
#### 3. >=1 phase / user story (in priority order)
TODO:
##### tests | user story's phase
* search ["Independent test"](example/specs/002-album-photo-sharing/tasks.md)
#### 4. Polish (cross-cutting concerns)
* [spec-002's Polish](example/specs/002-album-photo-sharing/tasks.md#phase-7-polish--cross-cutting-concerns)
### if it's POSSIBLE -> parallel execution
* check the `/speckit.tasks`'s output

# `/speckit.analyze`
* | [here](example)
  * `kiro-cli`
    * `/speckit.analyze`
## == consistency & quality analysis
* check the printed output
### read-only: ❌ NEVER edits files ❌
* check the printed output
### cross-artifact (`spec.md`, `plan.md`, `tasks.md`)
* check the output
### report DIFFERENT categories: consistency + ambiguities + underspecification + coverage gaps + duplication + constitution
* check the printed output
* `/speckit.clarify`
  * to fix the reported errors
## use cases
### BEFORE `/speckit.implement`
* | [here](example)
### AFTER `/speckit.implement`
TODO: 

# `/speckit.implement`
* | [here](example)
  * `kiro-cli`
    * `/speckit.implement`
      * ❌NOT possible❌
        * TODO: move to a dedicated repo
## executes tasks / specified | "tasks.md"
TODO:
### respect
#### dependency order
TODO:
#### parallel markers
TODO:
### -- based on the -- feature 
#### if it's small feature -> run it 1!
TODO:
#### if it's a large feature -> run in task' phases
TODO:

# `/speckit.converge`
TODO:
## responsible for: assess the codebase vs feature's spec + plan + tasks == confirm NOTHING was missed
TODO:
## use cases: AFTER `/speckit.implement` has run | CURRENT "tasks.md"
TODO:
## 's outcome: print a severity-graded findings summary
TODO:
### ✅ Converged == ❌ NO gaps found ❌
TODO:
#### "tasks.md" has NOT changed
TODO:
#### print: `✅ Converged — the implementation satisfies the spec, plan, and tasks.`
TODO:
#### NEXT steps: review OR open a PR
TODO:
### Tasks appended == gaps found
TODO:
#### add NEW tasks | "tasks.md"'s convergence section
TODO:
#### ❌ != edit OR delete code ❌
TODO:
#### NEXT steps: `/speckit.implement` → `/speckit.converge` again
TODO:
