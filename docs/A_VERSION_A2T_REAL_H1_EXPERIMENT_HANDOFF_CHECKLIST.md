# A2T Real H1 Experiment Handoff Checklist

Date: 2026-06-30

## Purpose

This checklist defines the remaining evidence required to close workstream 7:
transition from simulation-only A2T protocol governance to a real H1 hardware
metadata package.

H1 is not a discovery claim. H1 only means that the apparatus data, calibration
artifacts, and blind-analysis custody are complete enough to run the frozen
null-test analysis honestly.

## Current Status

```text
current_hardware_level = H0 simulation-only
h1_ready = false
hardware_claim_allowed = false
discovery_claim_allowed = false
```

## Required Files From The Experiment

The experiment team must provide:

```text
1. real apparatus event CSV
2. completed H1 manifest JSON
3. completed H1 acceptance matrix JSON
4. measured calibration artifact files referenced by the manifest
5. real pre-unblind analysis freeze hash
6. blind label map custody record
```

## Create A Shareable Request Package

Generate a folder that can be sent to the experiment team:

```text
python3 scripts/a2t_prepare_h1_request_package.py \
  --out-dir generated/h1_real_request_package_20260630
```

The package includes the event CSV template, manifest template, acceptance
matrix, handoff checklist, validator note, validator script, and a local
`README_H1_REQUEST.md`.

The template paths are:

```text
publication/a2t-null-test-report/data/hardware_h1_real_event_template.csv
publication/a2t-null-test-report/data/hardware_h1_real_intake_manifest_template.json
publication/a2t-null-test-report/data/hardware_h1_real_acceptance_matrix_template.json
```

## Required Event Schema

The event CSV must be nonempty and include all required fields listed in:

```text
publication/a2t-null-test-report/data/hardware_h1_real_intake_manifest_template.json
```

Critical field families:

```text
geometry and area vector
wavelength and wavelength calibration id
H/V/RCP/LCP polarization state and Stokes readout
temperature bias, temperature gradient, and dT/dt
previous geometry state, switch type, dummy switch, hold flag, wait time
platform orientation and measured/injected rotation rates
observed phase, uncertainty, visibility, detector saturation
blind offset id, blind label map version, analysis freeze hash
environment sidebands: pressure/vacuum, humidity, vibration, acoustic
laser frequency, laser power, beam position, settling monitors
```

## Required Calibration Families

Every calibration family must be apparatus-derived and marked:

```text
measured_hardware_pass
```

Required families:

```text
sagnac
polarization
wavelength_polarization
thermal_environment
mechanical_memory
laser_readout
blind
```

## Validator Command

After real files are supplied, run:

```text
python3 scripts/a2t_validate_hardware_metadata.py \
  --manifest <real_manifest.json> \
  --events <real_events.csv> \
  --out <validation_report.json>
```

## H1 Completion Marker

Workstream 7 is complete only if the validator returns:

```text
metadata_completeness = pass
calibration_artifacts = pass
blind_analysis = pass
h1_ready = true
hardware_claim_allowed = true
discovery_claim_allowed = false
```

Any placeholder, synthetic, TODO, missing, absent, or not-applicable calibration
status keeps the package below H1.

## Claim Boundary

Even if H1 passes:

```text
H1 = hardware metadata and calibration package ready for frozen analysis
H1 != hidden-flux detection
H1 != discovery
H1 != physical confirmation of A2T
```
