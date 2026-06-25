# From Higher-Dimensional Intuition to a Falsifiable A2T Null-Test: A Simulation and Experimental-Design Report

## Abstract

This report summarizes a research prototype that began as a higher-dimensional interpretation of light propagation and quantum interference, then progressively narrowed into a falsifiable phase-residual null-test called A2T. The current A2T formulation no longer treats photons as ordinary trajectories through an extra spatial dimension. Instead, it models a possible hidden internal/topological holonomy as an additional path phase, written phenomenologically as `delta_phi_hidden = -g_h Phi_h`, while preserving four-dimensional light-cone propagation. The project developed a simulation pipeline to separate such a hidden phase from known or likely false signals: Sagnac phase, polarization geometric phase, thermal/environmental drift, geometry-switch memory, delayed thermal response, and wavelength-dependent polarization effects. A final full milestone run with 49 scenarios, 80 trials, 36 blocks, run manifest, and calibration manifest produced `f_coverage_realistic ~= 1.6696`, dominated by block-bootstrap null risk rather than controlled-injection failure or post-gate nuisance leakage. The results support a stage-level conclusion: the simulation research prototype is internally closed for the current null-test design; it does not constitute experimental evidence for A2T.

## Keywords

A2T, hidden holonomy, topological flux, interferometry, null test, Sagnac calibration, polarization systematics, bootstrap coverage, simulation pipeline.

## 1. Introduction

The original conceptual question was whether the invariance of light speed and the structure of interference could be reinterpreted as a projection from a higher-dimensional process. Early analysis showed that ordinary extra-dimensional motion generally threatens four-dimensional light-cone behavior: if a photon carries velocity or momentum in an ordinary extra spatial dimension, its low-dimensional projection can acquire effective mass, dispersion, or Lorentz-violating signatures.

The working model therefore retreated from an ordinary Kaluza-Klein-like spatial path to an internal-fiber or hidden-holonomy interpretation. In this narrower A2T form, light remains on the four-dimensional null cone, while a hypothetical hidden connection could contribute an additional interferometric phase:

```text
delta_phi_hidden = -g_h Phi_h
```

The central scientific question becomes not whether this is elegant, but whether any residual phase can survive after known physical and instrumental effects are modeled or vetoed.

## 2. Model Reduction

The project considered several successive versions:

```text
Original A:
  Light propagates through ordinary higher-dimensional space.

A2 internal holonomy:
  Light propagates in four-dimensional spacetime, while phase/internal state evolves in a fiber.

A2T:
  A minimal hidden topological flux contributes only a path/area phase residual.
```

The original strong model was not retained as a serious formal claim because ordinary extra-dimensional motion tends to produce effective mass, birefringence, dispersion, or Lorentz violation. The surviving A2T version is therefore a phenomenological null-test target, not a proof of high-dimensional physics.

## 3. Null-Test Observable

The analysis focuses on an area-odd residual statistic:

```text
R_clean = R_raw - D_Sagnac - D_pol - D_env - D_memory - D_other
```

An A2T-like candidate must satisfy all of the following:

```text
1. It changes sign under area reversal.
2. It vanishes in zero-area controls.
3. It is not explained by Sagnac rotation.
4. It is not explained by polarization geometric phase or birefringence.
5. It is not explained by thermal, mechanical, environmental, or switch-memory effects.
6. It does not collapse under wavelength-scaling tests.
7. It preserves hidden-template identifiability after nuisance projection.
```

## 4. Simulation Pipeline

The main pipeline is `src/a2t_simulate_pipeline.py`. It uses only Python standard-library modules and generates simulated interferometric events across multiple systematic scenarios.

The current full profile includes 49 scenarios, including:

```text
null_clean
hidden_injection
sagnac_residual
polarization_residual
thermal_area_coupled
delayed_thermal_response
random_hysteresis
temperature_polarization_cross
lambda_waveplate_retardance
lambda_sp_phase_drift
lambda_birefringence_dispersion
lambda_qwp_retardance_error
lambda_polarimeter_basis_error
lambda_pmd
mixed_correlated
```

The simulation produces:

```text
a2t_simulation_summary.json
run_manifest.json
calibration_manifest.json
a2t_example_events.csv
```

## 5. Run Governance

The project separates routine and milestone analysis:

```text
filtered:
  default lightweight daily profile

pol-null:
  polarization null diagnostic profile

safety:
  Sagnac / thermal / memory regression profile

full:
  overnight or milestone profile
```

The authoritative run must satisfy:

```text
is_full_run = true
is_milestone_run = true
is_smoke_run = false
warning = null
calibration_status = pass
```

The authoritative milestone in this package satisfies those conditions.

## 6. Calibration Completeness

A separate calibration manifest tracks whether required metadata/calibrations are present. Missing calibration fields force an indeterminate status rather than allowing a false claim. For example, missing wavelength-dependent polarization calibration triggers:

```text
calibration_status = indeterminate
indeterminate_gates = [lambda_pol, pol_wavelength_null]
claim_policy = exploratory_residual_only
```

The authoritative milestone uses:

```text
calibration_status = pass
indeterminate_gates = []
covariance_components_missing = []
```

## 7. Conservative Coverage

Earlier versions separated null-channel widths from null-statistical diagnostics. The final milestone corrected this by defining:

```text
f_null_channel = max(null channel subcomponents)
f_null_statistical = max(null sigma model widths)
f_null = max(f_null_channel, f_null_statistical)
f_coverage_realistic = max(f_null, f_inj, f_sim, 1)
```

This prevents a statistical diagnostic such as block bootstrap from being reported but excluded from the final conservative upper-bound factor.

## 8. Milestone Results

Authoritative directory:

```text
generated/full_milestone_20260625_conservative_null_sigma
```

Run metadata:

```text
run_profile = full
scenario_source = run-profile:full
is_full_run = true
is_milestone_run = true
is_smoke_run = false
warning = null
calibration_status = pass
included_scenarios = 49
excluded_scenarios = 0
script_version = 4320062ad707
```

Coverage:

```text
f_coverage_realistic = 1.6696
f_null = 1.6696
f_null_channel = 1.2616
f_null_statistical = 1.6696
f_inj = 1.0284
f_sim = 1.0000
```

Dominant terms:

```text
dominant_null_component = f_pol_HV_wavelength_null_after_model
dominant_null_sigma_component = f_null_block_bootstrap
dominant_injection_component = f_thermal_inj
post_gate_nuisance_leakage_count = 0
```

Null sigma:

```text
f_null_gaussian = 1.0
f_null_empirical_95 = 1.0
f_null_student_t_proxy = 1.0
f_null_mixture_core = 1.0
f_null_hierarchical = 1.0730
f_null_block_bootstrap = 1.6696
null_tail_outlier_rate_3sigma = 0.0075
null_sigma_conclusion = null_sigma_model_adequate_after_component_scaling
```

Hidden injection:

```text
hidden_injection realistic_candidate_rate = 0.7625
hidden_identifiability_after_lambda_pol_model = 1.0
hidden_identifiability_after_pol_model = 1.0
hidden_identifiability_after_sagnac_model = 1.0
hidden_identifiability_after_pol_null_decomposition = 1.0
```

## 9. Conclusions by Research Line

### Line A: Lambda x Polarization Physical Model

The current milestone no longer shows a large wavelength-dependent polarization overdispersion after component-specific null sigma correction:

```text
f_pol_HV_wavelength_null_before_model ~= 1.2326
f_pol_HV_wavelength_null_after_model  ~= 1.2616
f_pol_RL_wavelength_null_after_model  ~= 1.0505
f_pol_lin_circ_wavelength_null_after_model = 1.0
```

Conclusion:

```text
Line A is stage-converged.
Current full evidence does not force an additional lambda-polarization physical term.
The full Jones/Mueller matrix chain remains future experiment-readiness work.
```

### Line B: Null Sigma / Heavy-Tail Modeling

The large earlier `f_null` values were traced to an incorrect diagnostic sigma: polarization and wavelength null differences had been normalized by scalar hidden-estimate `sigma_H` rather than by component-specific sample sigma. After correction, the authoritative milestone gives:

```text
null_sigma_conclusion = null_sigma_model_adequate_after_component_scaling
f_null_statistical = 1.6696
dominant_null_sigma_component = f_null_block_bootstrap
```

Conclusion:

```text
Line B is stage-converged.
The early large f_null was primarily a null-diagnostic sigma issue.
The final conservative coverage is now dominated by block-bootstrap family-wise risk.
```

### Line C: Calibration and Run Governance

Run manifest, calibration manifest, warning flags, profile policy, and indeterminate gates are implemented and verified.

Conclusion:

```text
Line C is complete for the simulation-prototype stage.
Real hardware metadata integration remains future work.
```

## 10. Limitations

This work has several important limits:

```text
1. It is a simulation and analysis-governance prototype, not an experimental detection.
2. The hidden phase is phenomenological and not derived from a full field theory.
3. The Jones/Mueller chain is still a reduced dispersion-basis model.
4. Full CSV event data is stored locally; this package includes a sample plus checksums.
5. Multiple-seed full milestone stability remains future work.
```

## 11. Data and Code Availability

The report package includes the pipeline source, selected research notes, run manifest, calibration manifest, reduced milestone summary, CSV sample, and checksums for the full local data.

The full local event CSV path is:

```text
generated/full_milestone_20260625_conservative_null_sigma/a2t_example_events.csv
```

## 12. Final Statement

The project has achieved research-prototype closure: A2T has been reduced to a falsifiable null-test, the main false-positive families have been structurally modeled, and the final milestone uses a conservative coverage factor. This does not validate the A2T hypothesis physically. It establishes a disciplined framework for rejecting or bounding it.
