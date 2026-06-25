# A2T calibration checklist

Status: condensed remote copy. The full working note is retained in the local publication bundle.

## Purpose

The calibration checklist defines which metadata and calibration fields must exist before an A2T residual can be treated as a candidate or upper-bound result rather than exploratory output.

## Major Calibration Groups

```text
sagnac:
  A_vec, platform orientation, injected rotation, earth rotation model

polarization:
  input/output polarimeter readout, extinction ratio, basis calibration

wavelength / lambda-pol:
  lambda center/drift/uncertainty, waveplate and QWP retardance(lambda), mirror/BS s-p phase(lambda, AOI), PMD(lambda)

thermal:
  temperature map, gradient, lag kernel, pressure, laser frequency

memory:
  previous geometry state, dummy switch flag, wait time, actuator readback

laser/readout:
  phase gain, visibility, detector saturation flag, phase uncertainty

blind analysis:
  blind offset id, analysis freeze hash, exclusion-rule version
```

## Gate Policy

If required calibration is missing, the pipeline must mark the relevant gate as `indeterminate` rather than reporting a candidate:

```text
missing lambda-pol calibration -> lambda_pol and pol_wavelength_null indeterminate
missing Sagnac calibration -> Sagnac gate indeterminate
missing thermal lag kernel -> delayed thermal gate indeterminate
missing geometry history -> memory gate indeterminate
missing blind freeze hash -> exploratory residual only
```

## Milestone Status

The authoritative milestone reports:

```text
calibration_status = pass
indeterminate_gates = []
covariance_components_missing = []
```

Conclusion: calibration governance is complete for the current simulation-prototype stage. Real hardware metadata integration remains future work.
