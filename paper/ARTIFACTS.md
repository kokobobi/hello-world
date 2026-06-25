# Artifact Map

## GitHub Uploaded Files

This repository is a selected publication bundle, not a complete executable mirror of the local workspace.

```text
README.md
paper/A2T_Null_Test_Report.md
paper/ARTIFACTS.md
src/PIPELINE_CHECKSUM.md
docs/A_VERSION_A2T_FULL_MILESTONE_AUDIT.md
docs/A_VERSION_INDEX.md
docs/A_VERSION_A2T_SIMULATION_SCHEMA.md
docs/A_VERSION_A2T_LAMBDA_POLARIZATION_PHYSICAL_MODEL.md
docs/A_VERSION_A2T_NULL_SIGMA_HEAVY_TAIL_MODEL.md
docs/A_VERSION_A2T_COMPONENT_SPECIFIC_NULL_SIGMA.md
docs/A_VERSION_A2T_CALIBRATION_CHECKLIST.md
docs/A_VERSION_A2T_RUN_POLICY.md
data/run_manifest.json
data/calibration_manifest.json
data/milestone_summary.json
data/a2t_example_events_sample.csv
data/FULL_DATA_CHECKSUMS.txt
```

## Authoritative Local Milestone

```text
generated/full_milestone_20260625_conservative_null_sigma
```

## Full Local Artifacts

The local publication bundle also contains fuller working notes and the milestone pipeline source:

```text
publication/a2t-null-test-report/
scripts/a2t_simulate_pipeline.py
generated/full_milestone_20260625_conservative_null_sigma/a2t_example_events.csv
```

## Checksums

```text
9025db95a1c16e1bf13239d2a32e7383defdd01f7a4bb19f3ac7418326c49043  a2t_simulation_summary.json
d7b2f94de7caace60e2025ab89716d3006941607fdc4a0144570d963f4e4ff7f  a2t_example_events.csv
c54bd7008a6a1b361f40786430d23e9b576057ce336dd89a84a667a30892d72c  run_manifest.json
69d5a7ed172a466f746a11ec0f258204d40b8ceac550aec691651a85cf5c61be  calibration_manifest.json
4320062ad70774f45bd742bac788ec5efaa504b158699f5295c2f6598712879a  a2t_simulate_pipeline.py
```

## Notes

The full event CSV is approximately 5.7 MB. It is retained locally and represented in this GitHub package by a sample CSV plus checksum.

The GitHub connector upload path used by Codex is optimized for UTF-8 text files and small-to-medium artifacts. The full CSV and full script can be added later through normal `git` or GitHub CLI authentication if an executable mirror is required.
