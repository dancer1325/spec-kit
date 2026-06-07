# My Preset

* goal
  * Example of how to create Spec Kit's CUSTOM preset

## Templates Included

| Template                 | Type     | Description                                                           |
|--------------------------|----------|-----------------------------------------------------------------------|
| `spec-template`          | template | Custom feature specification template (overrides core and extensions) |
| `myext-template`         | template | Override of the myext extension's report template                     |
| `speckit.specify`        | command  | Custom specification command (overrides core)                         |
| `speckit.myext.myextcmd` | command  | Override of the myext extension's myextcmd command                    |

## how to create a Preset?

* steps
  1. Copy this directory
     * `cp -r presets/scaffold my-preset`
  2. Edit `preset.yml`
     * == set your preset's ID + name + description + templates
  3. Add or modify templates | `templates/`
  4. Test locally
     * `specify preset add --dev ./my-preset`
  5. Verify resolution
     * `specify preset resolve spec-template`
  6. ONCE testing is done, remove it
     * `specify preset remove my-preset`

## "preset.yml"

* [source code](/spec-kit/src/specify_cli/presets.py)'s `PresetManifest`
