* goal
  * Spec Kit -- as -- SDD implementation

# Spec Kit's design

## Technology independence

* == create applications -- via -- DIFFERENT technology stacks OR programming languages OR frameworks

## Accepts constraints

* _Examples:_
  * organizational constraints (cloud providers, tech stacks, engineering practices)
  * compliance requirements

## Flexible -- to -- your preferences

* _Examples:_
  * support VARIOUS development approaches (vibe-coding, AI-native development, ...)

## iterative & parallel processes

* parallel processes
  * == generate >1 DIFFERENT implementations -- based on -- 1 specification
* iterative processes
  * == refine -- based on -- feedback loops

# Spec Kit's artifacts

* allow
  * implement SDD 

| Artifact      | Goal                              | File                              | SDD Principle                             | Produced by             |
|---------------|-----------------------------------|-----------------------------------|-------------------------------------------|-------------------------|
| Constitution  | Project principles and governance | `.specify/memory/constitution.md` | Rich specification with guardrails        | `/speckit.constitution` |
| Specification | Requirements & user scenarios     | `specs/<feature>/spec.md`         | Intent-driven: define *what* before *how* | `/speckit.specify`      |
| Plan          | Technical design & architecture   | `specs/<feature>/plan.md`         | Multi-step refinement (spec → plan)       | `/speckit.plan`         |
| Tasks         | Actionable implementation tasks   | `specs/<feature>/tasks.md`        | Specifications become executable          | `/speckit.tasks`        |
| Checklist     | Quality validation criteria       | `specs/<feature>/checklist.md`    | Rich specification with guardrails        | `/speckit.checklist`    |
