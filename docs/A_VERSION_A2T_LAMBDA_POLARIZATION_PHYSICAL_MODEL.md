# A2T lambda-polarization physical model v1

Status: condensed remote copy. The full working note is retained in the local publication bundle.

## Purpose

This note records the state of the wavelength-dependent polarization model used to test whether polarization dispersion could masquerade as an A2T hidden phase.

## Model Direction

The current simulation uses a reduced Jones/Mueller-inspired dispersion basis rather than a full optical matrix chain:

```text
waveplate_retardance(lambda)
mirror / beam splitter s-p phase(lambda, AOI)
linear_birefringence(lambda)
QWP retardance(lambda)
polarimeter basis(lambda)
PMD(lambda)
```

The basis is centered/normalized to avoid absorbing a wavelength-independent scalar hidden template.

## Hidden-Template Protection

The key identifiability check is:

```text
hidden_identifiability_after_lambda_pol_model
= ||(I - P_lambda_pol) h|| / ||h||
```

The milestone reports:

```text
hidden_identifiability_after_lambda_pol_model = 1.0
```

## Milestone Interpretation

With component-specific null sigma, the full milestone no longer shows large lambda-polarization overdispersion:

```text
f_pol_HV_wavelength_null_after_model ~= 1.2616
f_pol_RL_wavelength_null_after_model ~= 1.0505
f_pol_lin_circ_wavelength_null_after_model = 1.0
```

Conclusion: the current evidence does not force an additional lambda-polarization physical term. A full Jones/Mueller chain remains future experiment-readiness work, not a current blocker.
