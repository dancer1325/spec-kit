# 🔧 Specify CLI Reference

* [`specify <COMMAND_NAME>`](reference/core.md) 

## `/speckit.*` -- slash commands --

TODO: migrate to agentic-sdd.md

* requirements
  * have run `specify init`
* uses
  * 💡| your AI coding agent chat💡

### Core Commands

* == SDD workflow's essential commands 

| Command                 | Description                                                            |
| ----------------------- |------------------------------------------------------------------------|
| `/speckit.constitution` | Create OR update project governing principles & development guidelines |
| `/speckit.specify`      | Define what you want to build (requirements & user stories)            |
| `/speckit.plan`         | Create technical implementation plans / you choose tech stack          |
| `/speckit.tasks`        | Generate actionable task lists -- for -- implementation                |
| `/speckit.implement`    | Execute ALL tasks / build the feature -- based on the -- plan          |

### OPTIONAL Commands

* allows
  * enhance quality and validation

| Command              | Description                                                                                                                        |
| -------------------- |------------------------------------------------------------------------------------------------------------------------------------|
| `/speckit.clarify`   | Clarify underspecified areas <br/> recommended uses: BEFORE `/speckit.plan`                                                        |
| `/speckit.analyze`   | Cross-artifact consistency & coverage analysis <br/> uses: [AFTER `/speckit.tasks`, BEFORE `/speckit.implement`]                   |
| `/speckit.checklist` | Generate custom quality checklists / validate requirements completeness, clarity, and consistency |
