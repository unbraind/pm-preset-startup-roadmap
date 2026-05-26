# pm-preset-startup-roadmap

A [pm-cli](https://github.com/unbraind/pm-cli) extension that applies the **startup-roadmap** workspace preset — investor-grade milestones, strategic initiatives, and quarterly planning baked in from day one.

## What it does

Running `pm roadmap-setup` in a pm-cli workspace:

1. Writes a `settings.json` with the roadmap governance profile (strict metadata, progressive create mode, keyword search, month-first calendar).
2. Creates `.agents/pm/templates/` with three ready-to-use item templates.
3. Prints workflow guidance for the next steps.

## Install

```sh
pm install github.com/unbraind/pm-preset-startup-roadmap
```

> The `--project` flag scopes the extension to the current workspace only.

## Usage

```sh
pm roadmap-setup
```

Run from the root of a pm-cli workspace (the directory that contains `.agents/pm/`).

## Options

| Flag | Type | Description |
|------|------|-------------|
| `--force` | boolean | Overwrite an existing `settings.json` without prompting |
| `--dry-run` | boolean | Preview what would be written without making any changes |
| `--prefix <str>` | string | Override the `id_prefix` in settings (default: `road-`) |

## What gets installed

### Settings (`settings.json`)

| Setting | Value |
|---------|-------|
| `id_prefix` | `road-` |
| `governance.preset` | `default` |
| `governance.ownership_enforcement` | `warn` |
| `governance.create_mode_default` | `progressive` |
| `governance.close_validation_default` | `warn` |
| `governance.metadata_profile` | `strict` |
| `validation.sprint_release_format` | `warn` |
| `validation.parent_reference` | `warn` |
| `item_types` | Epic, Feature, Task |
| `search.mode` | `keyword` |
| `calendar.default_view` | `month` |
| `calendar.first_day_of_week` | `1` (Monday) |
| `telemetry.enabled` | `false` |

### Templates

#### `initiative.json` — Strategic Initiative (Epic)

Captures a top-level roadmap initiative with investor-visible fields:

- `objective`, `business_value`, `target_outcome`, `success_metrics`
- `owner`, `stakeholders`, `target_quarter`, `investment_level`
- `dependencies`, `risks`

#### `feature.json` — Product Feature

Ties a feature to a milestone with design and delivery metadata:

- `milestone`, `user_story`, `acceptance_criteria`, `business_value`
- `impacted_personas`, `owner`, `design_link`, `effort_estimate`, `dependencies`

#### `milestone.json` — Release Milestone

Tracks a release milestone with investor-facing and go-to-market fields:

- `target_date`, `release_name`, `scope_summary`, `exit_criteria`
- `owner`, `stakeholder_sign_off`, `investor_facing`, `go_to_market_notes`

## Startup workflow

```sh
# 1. Initialise a pm workspace (if you haven't already)
pm init

# 2. Install and apply the preset
pm install github.com/unbraind/pm-preset-startup-roadmap
pm roadmap-setup

# 3. Create your first strategic initiative
pm create --template initiative

# 4. Plan your first milestone
pm create --template milestone

# 5. Break the initiative into features
pm create --template feature

# 6. Review your roadmap in calendar view
pm calendar

# 7. List all investor-facing milestones
pm list --tag milestone
```

## Requirements

- `@unbrained/pm-cli` >= 2026.5.0

## License

MIT

## Release Automation

This package is release-ready for GitHub, npm, and Bun-compatible installs. CI runs type checking, build, production dependency audit, package packing, Bun install verification, and pm-changelog validation. The daily release workflow publishes only when commits exist after the latest release tag and uses pm-changelog to generate CHANGELOG.md and GitHub release notes.
