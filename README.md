# A2T Hidden Topological Flux Null-Test

This repository hosts the A2T null-test research package and current handoff/status materials.

A2T began as a high-dimensional light-projection intuition and has been narrowed into a conservative, falsifiable interferometric path-phase null-test framework:

```text
delta_phi_total = delta_phi_QM + delta_phi_known + delta_phi_hidden
delta_phi_hidden = -g_h Phi_h
```

## Current Status

As of the latest local audit, this is **simulation-governance work only**:

```text
hidden dimensions proven = false
hidden flux detected = false
hardware H1 ready = false
discovery claim allowed = false
```

Seven-item goal audit:

```text
goal_complete = false
completed_item_count = 5 / 7
items 1-5 = complete/pass locally
item 6 = local publication package complete, GitHub git-level remote verification still incomplete
item 7 = H1 handoff package exists, real apparatus data still missing
```

## Current Local Publication Package

The authoritative local publication package is maintained outside this remote as a git bundle:

```text
publication HEAD = 66694666bb0b9f13aa7dca2ad62cba8fe36ad643
tag = local-publication-20260630
bundle sha256 = 375a97bc4fcf3930d8f1505f5388de71d21d44ee4c26c5c86afd2a9bb3b6ac4c
bundle clone verified = true
```

This GitHub repository has connector-updated status files, but it is **not yet verified as a full git remote mirror** of the local publication package because local `git push` authentication is unavailable in the current shell.

## Key Status Files

- [data/seven_item_goal_audit_20260630.json](data/seven_item_goal_audit_20260630.json)
- [data/remote_upload_readiness_final_20260630.json](data/remote_upload_readiness_final_20260630.json)
- [docs/A_VERSION_A2T_SEVEN_ITEM_GOAL_AUDIT_RUNNER.md](docs/A_VERSION_A2T_SEVEN_ITEM_GOAL_AUDIT_RUNNER.md)
- [docs/A_VERSION_A2T_REMOTE_PUBLICATION_HANDOFF_CHECKLIST.md](docs/A_VERSION_A2T_REMOTE_PUBLICATION_HANDOFF_CHECKLIST.md)
- [docs/A_VERSION_A2T_REAL_H1_EXPERIMENT_HANDOFF_CHECKLIST.md](docs/A_VERSION_A2T_REAL_H1_EXPERIMENT_HANDOFF_CHECKLIST.md)

## Completion Markers

Workstream 6 is complete only after a passing remote verification report proves the GitHub branch/tag match the local final manifest.

Workstream 7 is complete only after real apparatus events, measured calibration artifacts, and blind-analysis custody pass the H1 validator.

Until both happen, the correct project status is:

```text
simulation protocol passed
local publication package prepared
remote git-level publication unverified
H1 hardware readiness false
hardware/discovery claim disallowed
```
