# Initialize a NEW Project
## about project name
### 1. <PROJECT_NAME>
* `uvx --from git+https://github.com/github/spec-kit.git specify init specifyProjectName`
  * create [specifyProjectName/](specifyProjectName/)
* check
  * [commands / AVAILABLE | your AI agent](specifyProjectName/.claude/commands)
  * [".specify/scripts/"](specifyProjectName/.specify/scripts)
### 2. | CURRENT directory
* `mkdir directoryCreatedManually`
* `uvx --from git+https://github.com/github/spec-kit.git specify init .`
* check
  * [commands / AVAILABLE | your AI agent](directoryCreatedManually/.claude/commands)
  * [".specify/scripts/"](directoryCreatedManually/.specify/scripts)
### 3. --here
* `mkdir anotherDirectoryCreatedManually`
* `uvx --from git+https://github.com/github/spec-kit.git specify init .`
* check
  * [commands / AVAILABLE | your AI agent](anotherDirectoryCreatedManually/.claude/commands)
  * [".specify/scripts/"](anotherDirectoryCreatedManually/.specify/scripts)
## + specify AI Agent -- via -- `--ai`
* `uvx --from git+https://github.com/github/spec-kit.git specify init specifyAIAgent --ai claude`
  * create [specifyAIAgent/](specifyAIAgent/)
* check
  * [commands / AVAILABLE | your AI agent](specifyAIAgent/.claude/commands)
  * [".specify/scripts/"](specifyAIAgent/.specify/scripts)
## + specify AI Agent -- via -- `--ai`
* `uvx --from git+https://github.com/github/spec-kit.git specify init specifyAIAgent --ai claude`
  * create [specifyAIAgent/](specifyAIAgent/)
* check
  * [commands / AVAILABLE | your AI agent](specifyAIAgent/.claude/commands)
  * [".specify/scripts/"](specifyAIAgent/.specify/scripts)
## + specify script type (Shell vs PowerShell) -- via -- `--script`
* `uvx --from git+https://github.com/github/spec-kit.git specify init specifyScript --script sh`
  * create [specifyScript/](specifyScript/)
* check
  * [commands / AVAILABLE | your AI agent](specifyScript/.claude/commands)
  * [".specify/scripts/"](specifyScript/.specify/scripts)
## + ignore Agent Tools check -- via -- `--ignore-agent-tools`
* `uvx --from git+https://github.com/github/spec-kit.git specify init ignoreAgentTools --ignore-agent-tools`
  * create [ignoreAgentTools/](ignoreAgentTools/)
* check
  * [commands / AVAILABLE | your AI agent](ignoreAgentTools/.claude/commands)
  * [".specify/scripts/"](ignoreAgentTools/.specify/scripts)
  * [".specify/templates/"](ignoreAgentTools/.specify/templates)
