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

```bash
/speckit.clarify Focus on security and performance requirements.
```

### create a technical implementation plan

* | claude chat
  * `/speckit.plan provideYourTechStackAndArchiteChoices`

```bash
/speckit.plan The application uses Vite with minimal number of libraries
* Use vanilla HTML, CSS, and JavaScript as much as possible
* Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

### break down into tasks

* | claude chat
  * `/speckit.tasks` 
    * FROM your implementation plan, create an actionable task list 

### validate the plan

* OPTIONAL
* | claude chat
  * `/speckit.analyze`

### execute implementation

* | claude chat
  * `/speckit.implement`
    * execute ALL tasks
    * build your feature -- based on the -- plan

## Detailed Example: Building Taskify

Here's a complete example of building a team productivity platform:

### Step 1: Define Constitution

Initialize the project's constitution to set ground rules:

```markdown
/speckit.constitution Taskify is a "Security-First" application. All user inputs must be validated. We use a microservices architecture. Code must be fully documented.
```

### Step 2: Define Requirements with `/speckit.specify`

```text
Develop Taskify, a team productivity platform. It should allow users to create projects, add team members,
assign tasks, comment and move tasks between boards in Kanban style. In this initial phase for this feature,
let's call it "Create Taskify," let's have multiple users but the users will be declared ahead of time, predefined.
I want five users in two different categories, one product manager and four engineers. Let's create three
different sample projects. Let's have the standard Kanban columns for the status of each task, such as "To Do,"
"In Progress," "In Review," and "Done." There will be no login for this application as this is just the very
first testing thing to ensure that our basic features are set up.
```

### Step 3: Refine the Specification

Use the `/speckit.clarify` command to interactively resolve any ambiguities in your specification. You can also provide specific details you want to ensure are included.

```bash
/speckit.clarify I want to clarify the task card details. For each task in the UI for a task card, you should be able to change the current status of the task between the different columns in the Kanban work board. You should be able to leave an unlimited number of comments for a particular card. You should be able to, from that task card, assign one of the valid users.
```

You can continue to refine the spec with more details using `/speckit.clarify`:

```bash
/speckit.clarify When you first launch Taskify, it's going to give you a list of the five users to pick from. There will be no password required. When you click on a user, you go into the main view, which displays the list of projects. When you click on a project, you open the Kanban board for that project. You're going to see the columns. You'll be able to drag and drop cards back and forth between different columns. You will see any cards that are assigned to you, the currently logged in user, in a different color from all the other ones, so you can quickly see yours. You can edit any comments that you make, but you can't edit comments that other people made. You can delete any comments that you made, but you can't delete comments anybody else made.
```

### Step 4: Validate the Spec

Validate the specification checklist using the `/speckit.checklist` command:

```bash
/speckit.checklist
```

### Step 5: Generate Technical Plan with `/speckit.plan`

Be specific about your tech stack and technical requirements:

```bash
/speckit.plan We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API, tasks API, and a notifications API.
```

### Step 6: Validate and Implement

Have your AI agent audit the implementation plan using `/speckit.analyze`:

```bash
/speckit.analyze
```

Finally, implement the solution:

```bash
/speckit.implement
```

## Key Principles

- **Be explicit** about what you're building and why
- **Don't focus on tech stack** during specification phase
- **Iterate and refine** your specifications before implementation
- **Validate** the plan before coding begins
- **Let the AI agent handle** the implementation details

## Notes

- _Examples:_ [here](../templates)
