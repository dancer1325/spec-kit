<div align="center">
    <img src="./media/logo_large.webp" alt="Spec Kit Logo" width="200" height="200"/>
    <h1>🌱 Spec Kit</h1>
</div>

* == SDD toolkit -- for -- AI coding agents
  * open source
  * allows you to
    * 👀focus | product scenarios & predictable outcomes👀
      * ❌!= vibe coding EACH piece -- from -- scratch❌
    * building high-quality software faster
  * [goal](docs/goals.md)

## Documentation
* [here](docs/index.md)
* [Video Overview](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)
  * TODO: 
* [SDD](spec-driven.md)


TODO: check

## 🔧 Specify CLI Reference

For full command details, options, and examples, see the [CLI Reference](https://github.github.io/spec-kit/reference/overview.html).

## 🧩 Making Spec Kit Your Own: Extensions & Presets

Spec Kit can be tailored to your needs through two complementary systems — **extensions** and **presets** — plus project-local overrides for one-off adjustments:

| Priority | Component Type                                    | Location                         |
| -------: | ------------------------------------------------- | -------------------------------- |
|      ⬆ 1 | Project-Local Overrides                           | `.specify/templates/overrides/`  |
|        2 | Presets — Customize core & extensions             | `.specify/presets/templates/`    |
|        3 | Extensions — Add new capabilities                 | `.specify/extensions/templates/` |
|      ⬇ 4 | Spec Kit Core — Built-in SDD commands & templates | `.specify/templates/`            |

- **Templates** are resolved at **runtime** — Spec Kit walks the stack top-down and uses the first match.
- Project-local overrides (`.specify/templates/overrides/`) let you make one-off adjustments for a single project without creating a full preset.
- **Extension/preset commands** are applied at **install time** — when you run `specify extension add` or `specify preset add`, command files are written into agent directories (e.g., `.claude/commands/`).
- If multiple presets or extensions provide the same command, the highest-priority version wins. On removal, the next-highest-priority version is restored automatically.
- If no overrides or customizations exist, Spec Kit uses its core defaults.

### Extensions — Add New Capabilities

Use **extensions** when you need functionality that goes beyond Spec Kit's core. Extensions introduce new commands and templates — for example, adding domain-specific workflows that are not covered by the built-in SDD commands, integrating with external tools, or adding entirely new development phases. They expand *what Spec Kit can do*.

```bash
# Search available extensions
specify extension search

# Install an extension
specify extension add <extension-name>
```

For example, extensions could add Jira integration, post-implementation code review, V-Model test traceability, or project health diagnostics.

See the [Extensions reference](https://github.github.io/spec-kit/reference/extensions.html) for the full command guide. Browse the [community extensions](https://github.github.io/spec-kit/community/extensions.html) for what's available.

### Presets — Customize Existing Workflows

Use **presets** when you want to change *how* Spec Kit works without adding new capabilities. Presets override the templates and commands that ship with the core *and* with installed extensions — for example, enforcing a compliance-oriented spec format, using domain-specific terminology, or applying organizational standards to plans and tasks. They customize the artifacts and instructions that Spec Kit and its extensions produce.

```bash
# Search available presets
specify preset search

# Install a preset
specify preset add <preset-name>
```

For example, presets could restructure spec templates to require regulatory traceability, adapt the workflow to fit the methodology you use (e.g., Agile, Kanban, Waterfall, jobs-to-be-done, or domain-driven design), add mandatory security review gates to plans, enforce test-first task ordering, or localize the entire workflow to a different language. The [pirate-speak demo](https://github.com/mnriem/spec-kit-pirate-speak-preset-demo) shows just how deep the customization can go. Multiple presets can be stacked with priority ordering.

See the [Presets reference](https://github.github.io/spec-kit/reference/presets.html) for the full command guide, including resolution order and priority stacking.

## 📦 Bundles: Role-Based Setups

Extensions and presets are individual building blocks. A **bundle** packages a
curated set of them — extensions, presets, steps, and workflows — into a single,
versioned, role-oriented setup so a whole team persona (product manager, business
analyst, security researcher, developer, …) can be provisioned with one command.

A bundle is described by a hand-written `bundle.yml` manifest. It pins each
component to a version and, optionally, targets a specific integration; a bundle
with no `integration` is **agnostic** and inherits whatever integration the
project already uses.

```bash
# Discover bundles in the active catalog stack
specify bundle search [<query>]

# Inspect the exact component set a bundle will add (equals what install does)
specify bundle info <bundle-id>

# Install a bundle's full component set in one operation
specify bundle install <bundle-id>

# See what's installed, then update or remove non-destructively
specify bundle list
specify bundle update <bundle-id>     # or --all
specify bundle remove <bundle-id>     # removes only this bundle's components
```

Bundles resolve from a **priority-ordered catalog stack** (project > user >
built-in). Each source carries an install policy: `install-allowed` sources can
be installed from, while `discovery-only` sources are visible in `search`/`info`
but refuse installation. Manage the stack with `specify bundle catalog list|add|remove`.

Authors validate and package bundles locally. Distribution is hosting the built
artifact and adding a catalog source; community bundle submissions use the
[Bundle Submission](https://github.com/github/spec-kit/issues/new?template=bundle_submission.yml)
issue template so required component catalogs and install evidence can be reviewed:

```bash
specify bundle validate --path ./my-bundle      # structural + reference checks
specify bundle build --path ./my-bundle         # produce a versioned .zip artifact
```

Four ready-to-read example manifests live under
[`examples/bundles/`](examples/bundles/) (product manager, business analyst,
security researcher, developer).

Key guarantees: `info` shows exactly what `install` adds (transparency);
installs are idempotent and confined to the project root; `remove` never touches
components another installed bundle still needs; and all consume/author commands
work **offline** against local or pinned sources.

### When to Use Which

| Goal | Use |
| --- | --- |
| Add a brand-new command or workflow | Extension |
| Customize the format of specs, plans, or tasks | Preset |
| Integrate an external tool or service | Extension |
| Enforce organizational or regulatory standards | Preset |
| Ship reusable domain-specific templates | Either — presets for template overrides, extensions for templates bundled with new commands |
| Provision a complete role-based setup in one command | Bundle |

## 📚 Core Philosophy

Spec-Driven Development is a structured process that emphasizes:

- **Intent-driven development** where specifications define the "*what*" before the "*how*"
- **Rich specification creation** using guardrails and organizational principles
- **Multi-step refinement** rather than one-shot code generation from prompts
- **Heavy reliance** on advanced AI model capabilities for specification interpretation
