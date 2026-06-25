# A2T null sigma and heavy-tail model

Status: condensed remote copy. The full working note is retained in the local publication bundle.

## Purpose

This note tracks why early A2T null-channel coverage factors became very large and how the pipeline separated true physical-model risk from statistical normalization error, heavy tails, block variance, and family-wise null risk.

## Key Correction

Early polarization and wavelength null diagnostics normalized component differences by scalar `sigma_H`. That was too narrow for H/V, RCP/LCP, linear/circular, and wavelength-cross differences.

The corrected pipeline uses component-specific null sigma:

```text
f_null = max(f_null_channel, f_null_statistical)
f_coverage_realistic = max(f_null, f_inj, f_sim, 1)
```

Statistical diagnostics include:

```text
f_null_gaussian
f_null_empirical_95
f_null_student_t_proxy
f_null_mixture_core
f_null_block_bootstrap
f_null_hierarchical
```

## Milestone Conclusion

The authoritative full milestone reports:

```text
null_sigma_conclusion = null_sigma_model_adequate_after_component_scaling
f_null_statistical = 1.6696
dominant_null_sigma_component = f_null_block_bootstrap
```

Interpretation: the early huge `f_null` was primarily a diagnostic-sigma issue. The final conservative factor is dominated by block-bootstrap family-wise risk, not by a forced new lambda-polarization physical term.
