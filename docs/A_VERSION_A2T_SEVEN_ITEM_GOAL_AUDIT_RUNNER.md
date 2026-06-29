# A2T Seven-Item Goal Audit Runner

Date: 2026-06-30

## Purpose

The project now has many local artifacts, but the active goal is broader than
local artifact creation. This runner converts the seven-item completion audit
into a machine-checkable status report.

It is intentionally conservative:

```text
local publication package != GitHub remote publication
H1 template package != real H1 hardware readiness
```

## Script

```text
scripts/a2t_audit_seven_item_goal.py
publication/a2t-null-test-report/src/a2t_audit_seven_item_goal.py
```

## Default Command

```text
python3 scripts/a2t_audit_seven_item_goal.py \
  --out generated/seven_item_goal_audit_20260630.json \
  --h1-validation-out generated/seven_item_h1_validation_20260630.json
```

By default the script does not contact GitHub. It uses the local final manifest
and the H1 template validator.

## Remote Completion Input

After GitHub upload is performed, pass a remote verification report:

```text
python3 scripts/a2t_verify_remote_publication.py \
  --repository-full-name kokobobi/<repo-name> \
  --out generated/remote_publication_verification_20260630.json

python3 scripts/a2t_audit_seven_item_goal.py \
  --remote-verification-report generated/remote_publication_verification_20260630.json \
  --out generated/seven_item_goal_audit_20260630.json
```

## H1 Completion Input

After real apparatus files are supplied, pass the completed manifest and event
CSV:

```text
python3 scripts/a2t_audit_seven_item_goal.py \
  --h1-manifest <real_manifest.json> \
  --h1-events <real_events.csv> \
  --h1-validation-out generated/real_h1_validation_report.json \
  --out generated/seven_item_goal_audit_20260630.json
```

## Completion Semantics

The runner reports `goal_complete = true` only when:

```text
items 1-5 have accepted local evidence;
item 6 has local package verification and remote GitHub verification;
item 7 has h1_ready=true from the hardware metadata validator.
```

Current expected state before external inputs:

```text
goal_complete = false
completed_item_count = 5
remaining = GitHub remote verification + real H1 hardware package
```
