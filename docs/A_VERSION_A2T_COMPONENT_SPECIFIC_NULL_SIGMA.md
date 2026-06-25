# A2T component-specific null sigma

Status: condensed remote copy. The full working note is retained in the local publication bundle.

## Background

The A2T pipeline originally normalized multiple null-channel differences with scalar hidden-estimate uncertainty `sigma_H`. That produced artificially large z-scores for polarization and wavelength null channels.

## Correction

The pipeline now uses component-specific sample uncertainty for each diagnostic family:

```text
pol_hv_block_sigma
pol_rl_block_sigma
pol_lin_circ_block_sigma
pol_hv_lambda_cross_sigma
pol_rl_lambda_cross_sigma
pol_lin_circ_lambda_cross_sigma
lambda_signed_sigma
```

This changed the interpretation of earlier huge null factors.

## Validation Outcome

After the correction, targeted runs no longer supported the earlier diagnosis that a large missing lambda-polarization physical term was forced by the data. The full milestone gives:

```text
f_coverage_realistic ~= 1.6696
f_null_channel ~= 1.2616
f_null_statistical ~= 1.6696
null_sigma_conclusion = null_sigma_model_adequate_after_component_scaling
```

## Conclusion

Component-specific null sigma closed the main statistical normalization problem. Remaining conservative coverage is driven by block-level family-wise risk rather than a single leaking nuisance scenario.
