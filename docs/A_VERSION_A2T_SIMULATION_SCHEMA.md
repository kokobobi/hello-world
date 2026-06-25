# A2T simulation schema

Status: condensed remote schema. The full local schema remains in the publication bundle.

## Main Outputs

```text
a2t_simulation_summary.json
run_manifest.json
calibration_manifest.json
a2t_example_events.csv
```

## Key Summary Fields

```text
run_profile
scenario_source
is_full_run
is_milestone_run
is_smoke_run
warning
calibration_status
included_scenarios
f_coverage_realistic
f_null
f_null_channel
f_null_statistical
f_inj
f_sim
dominant_null_component
dominant_null_sigma_component
post_gate_nuisance_leakage_count
hidden_identifiability_after_lambda_pol_model
hidden_identifiability_after_pol_model
hidden_identifiability_after_sagnac_model
hidden_identifiability_after_pol_null_decomposition
```

## Event Table Families

The CSV event table records simulated interferometric events with fields covering:

```text
geometry and area sign
previous geometry / switch memory
wavelength
polarization
effective area and rotation terms
Sagnac proxies
polarization and wavelength bases
temperature / pressure / humidity / vibration / acoustic metadata
laser frequency and alignment metadata
thermal lag and hysteresis states
platform orientation
observed phase and decomposed true/model phase terms
```

## Scenario Families

The full profile includes 49 scenarios, spanning:

```text
null and hidden injection
Sagnac residuals and Sagnac calibration injections
polarization residuals and controlled polarization injections
thermal/environmental drift
thermal-area coupling
delayed thermal response
geometry-switch memory/random hysteresis
wavelength calibration and lambda-polarization dispersion
mixed correlated systematics
```

## Governance

A result is milestone-grade only when:

```text
run_profile = full
is_full_run = true
is_milestone_run = true
warning = null
calibration_status = pass
```
