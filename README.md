# A2T Hidden Topological Flux Null-Test

This repository contains a research-style report and supporting artifacts for the A2T project: a speculative higher-dimensional/light-projection intuition reduced into a falsifiable interferometric null-test framework.

The current conclusion is conservative: the project does not prove hidden dimensions or a hidden topological flux. It produces a disciplined null-test design, simulation pipeline summary, calibration manifests, and a milestone result showing that the strongest current claim is an upper-bound framework, not a discovery claim.

## Main Report

- [paper/A2T_Null_Test_Report.md](paper/A2T_Null_Test_Report.md)
- [paper/ARTIFACTS.md](paper/ARTIFACTS.md)

## Key Data Materials

- [data/milestone_summary.json](data/milestone_summary.json)
- [data/run_manifest.json](data/run_manifest.json)
- [data/calibration_manifest.json](data/calibration_manifest.json)
- [data/FULL_DATA_CHECKSUMS.txt](data/FULL_DATA_CHECKSUMS.txt)
- [data/a2t_example_events_sample.csv](data/a2t_example_events_sample.csv)

The full local event table is intentionally represented here by checksum and a small sample. The milestone full CSV is about 5.7 MB locally and can be added later through normal git/gh authentication if needed.

## Supporting Docs

- [docs/A_VERSION_A2T_FULL_MILESTONE_AUDIT.md](docs/A_VERSION_A2T_FULL_MILESTONE_AUDIT.md)
- [docs/A_VERSION_A2T_NULL_SIGMA_HEAVY_TAIL_MODEL.md](docs/A_VERSION_A2T_NULL_SIGMA_HEAVY_TAIL_MODEL.md)
- [docs/A_VERSION_A2T_COMPONENT_SPECIFIC_NULL_SIGMA.md](docs/A_VERSION_A2T_COMPONENT_SPECIFIC_NULL_SIGMA.md)
- [docs/A_VERSION_A2T_LAMBDA_POLARIZATION_PHYSICAL_MODEL.md](docs/A_VERSION_A2T_LAMBDA_POLARIZATION_PHYSICAL_MODEL.md)
- [docs/A_VERSION_A2T_CALIBRATION_CHECKLIST.md](docs/A_VERSION_A2T_CALIBRATION_CHECKLIST.md)
- [docs/A_VERSION_A2T_RUN_POLICY.md](docs/A_VERSION_A2T_RUN_POLICY.md)
- [src/PIPELINE_CHECKSUM.md](src/PIPELINE_CHECKSUM.md)

## Current Milestone Snapshot

- Full milestone directory: `generated/full_milestone_20260625_conservative_null_sigma`
- Run profile: `full`
- Calibration status: `pass`
- Included scenarios: `49`
- Realistic coverage factor: `1.6696`
- Dominant null component: `f_pol_HV_wavelength_null_after_model`
- Post-gate nuisance leakage count: `0`
- Hidden-injection realistic candidate rate: `0.7625`

## Scientific Status

The A2T hypothesis has been narrowed from a broad higher-dimensional interpretation into a minimal path-phase null-test:

```text
delta_phi_total
= delta_phi_QM
+ delta_phi_known
+ delta_phi_hidden

delta_phi_hidden = - g_h Phi_h
```

The milestone result supports the following cautious statement:

> No hidden-flux discovery is claimed. The current deliverable is a reproducible null-test framework and a conservative upper-bound procedure after Sagnac, polarization, thermal, memory, delayed-thermal, and null-channel diagnostics.
