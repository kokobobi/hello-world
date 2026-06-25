# A2T run policy

Status: condensed remote copy. The full working note is retained in the local publication bundle.

## Purpose

The run policy prevents accidental confusion between smoke tests, filtered daily runs, focused diagnostics, and milestone full runs.

## Profile Precedence

```text
scenario-filter > run-profile > default filtered
```

If `--scenario-filter` is present, it overrides `--run-profile`.

## Profiles

```text
filtered:
  default lightweight daily profile

pol-null:
  focused polarization and wavelength null diagnostics

safety:
  Sagnac / thermal / memory regression checks

full:
  overnight or milestone profile
```

## Milestone Criteria

A result can be treated as the authoritative milestone only if:

```text
run_profile = full
is_full_run = true
is_milestone_run = true
is_smoke_run = false
warning = null
calibration_status = pass
```

## Manifest Requirement

Every run writes a `run_manifest.json` containing:

```text
run_profile
scenario_filter
scenario_source
profile_precedence
trials
blocks
seed
timestamp
script_version
included_scenarios
excluded_scenarios
output_directory
is_full_run
is_milestone_run
is_smoke_run
warning_if_not_full
```

This prevents filtered or smoke results from being mistaken for final coverage evidence.
