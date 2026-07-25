# CLI Reference -- `specify` --

* 💡manages the SDD infrastructure💡
  * _Examples:_ Spec Kit project initialization, agent integrations, extensions, ...
  * ❌!= SDD phases❌
    * Reason:🧠those are managed -- via -- [slash commands](/spec-kit/templates/commands)🧠

* types of commands
  * [core](core.md)
  * [authentication](authentication.md)
  * [extensions](extensions.md)
  * [integrations](integrations.md)
  * [presets](presets.md)
  * [workflows](workflows.md)
  * TODO: add rest 


## Bundles

Bundles compose existing extensions, presets, workflows, and steps into a single, versioned, installable unit. Rather than adding new behavior, a bundle curates a stack of primitives — everything a team or role needs — and installs it in one step through each component's own machinery, with version pinning, conflict checks, and provenance tracking for clean updates and removal.

[Bundles reference →](bundles.md)

## Agentic Commands

The sections above cover primitives managed by the `specify` CLI. The following are the `/speckit.*` slash commands your coding agent runs step by step inside the editor — the agentic processes built on top of that foundation.

### Agentic SDD

The `/speckit.*` slash commands that drive the core Spec-Driven Development process your coding agent runs step by step: constitution, specify, clarify, plan, checklist, tasks, analyze, implement, and converge. Run them in order, adding the clarify/checklist/analyze quality gates for anything with meaningful ambiguity.

[Agentic SDD reference →](agentic-sdd.md)

### Agentic Bug Fix

The bundled **bug** extension adds a three-step bug triage process — assess, fix, and validate — with each bug tracked in its own directory under `.specify/bugs/`. Install it with `specify extension add bug`.

[Agentic Bug Fix reference →](agentic-bugfix.md)
