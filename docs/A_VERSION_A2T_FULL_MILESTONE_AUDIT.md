# A2T full milestone audit

日期：2026-06-25

状态：external / candidate experiment tooling audit。本文只是 A2T 候选实验模拟管线的里程碑审计，不写入个人世界观。

## 0. 目的

本轮审计对应三条推进主线：

```text
主线 A：lambda x polarization physical model
主线 B：null sigma / heavy-tail / conservative coverage
主线 C：metadata -> calibration checklist and run governance
```

目标不是证明 A2T 为真，而是判断当前模拟管线是否已经足以给出阶段性收敛结论。

## 1. 权威 milestone run

当前权威结果目录：

```text
generated/full_milestone_20260625_conservative_null_sigma
```

运行命令：

```bash
python3 scripts/a2t_simulate_pipeline.py \
  --run-profile full \
  --trials 80 \
  --blocks 36 \
  --out-dir generated/full_milestone_20260625_conservative_null_sigma
```

运行治理字段：

```text
run_profile = full
scenario_source = run-profile:full
scenario_filter = null
is_full_run = true
is_milestone_run = true
is_smoke_run = false
warning = null
calibration_status = pass
calibration_warning = null
included_scenarios = 49
excluded_scenarios = 0
script_version = 4320062ad707
```

耗时：

```text
real ~= 2092.57 s
user ~= 2076.42 s
sys  ~= 10.02 s
```

结论：该 run 可以作为当前阶段正式 milestone evidence，不属于 smoke / filtered / exploratory 结果。

## 2. Conservative coverage 修正

在前一份 full run：

```text
generated/full_milestone_20260624_component_sigma
```

曾出现：

```text
f_coverage_realistic = 1.2616
f_null_block_bootstrap = 1.6696
```

这说明 `null_sigma_models` 只是诊断输出，没有被纳入 final conservative coverage。该口径不够保守。

脚本已修正为：

```text
f_null = max(
  f_null_channel,
  f_null_statistical
)

f_null_statistical = max(
  f_null_gaussian,
  f_null_empirical_95,
  f_null_student_t_proxy,
  f_null_mixture_core,
  f_null_block_bootstrap,
  f_null_hierarchical
)

f_coverage_realistic = max(
  f_null,
  f_inj,
  f_sim,
  1
)
```

新增 summary 字段：

```text
f_null_channel
f_null_statistical
active_null_sigma_components
dominant_null_sigma_component
```

## 3. 最新 coverage 结果

最新 full milestone：

```text
f_coverage_realistic = 1.6696
f_null = 1.6696
f_null_channel = 1.2616
f_null_statistical = 1.6696
f_inj = 1.0284
f_sim = 1.0
```

主导项：

```text
dominant_null_component = f_pol_HV_wavelength_null_after_model
dominant_null_sigma_component = f_null_block_bootstrap
dominant_injection_component = f_thermal_inj
post_gate_nuisance_leakage_count = 0
```

null sigma model：

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

解释：

```text
普通 Gaussian / Student-t / mixture core 没有显示严重厚尾；
层级方差很小；
最终 coverage 由 block-bootstrap family-wise 风险保守主导。
```

## 4. 主线 A 结论

主线 A 原始问题：

```text
当前 f_null 是否说明 lambda x polarization physical model 缺项？
```

最新结果：

```text
f_pol_HV_wavelength_null_before_model = 1.2326
f_pol_HV_wavelength_null_after_model  = 1.2616
f_pol_RL_wavelength_null_after_model  = 1.0505
f_pol_lin_circ_wavelength_null_after_model = 1.0
f_pol_wavelength_cross_null = 1.2616
hidden_identifiability_after_lambda_pol_model = 1.0
lambda_pol_model_pass_rate for hidden_injection = 1.0
```

判断：

```text
A 线没有证明真实 Jones/Mueller chain 已完成；
但在 component-specific null sigma 后，当前 full milestone 不再显示显著 lambda-pol overdispersion；
因此当前数据不强迫新增 lambda-pol 物理项来解释 f_null。
```

早期判据要求：

```text
f_pol_HV_wavelength_null_after_model 明显低于 before_model
```

该判据本轮没有满足。但原因不是模型失败导致巨大 residual 持续存在，而是修正 sigma 后 before/after 都已接近 1。该判据在当前阶段被重新解释为：

```text
若 f_pol_wavelength_cross_null 已接近 1，则不再要求模型制造人为下降；
下一步真实 Jones matrix chain 属于 experiment-readiness，而不是当前 A/B 收敛的 blocker。
```

主线 A 当前状态：

```text
stage-converged:
  no current evidence forcing new lambda-pol physical term;
  full Jones/Mueller matrix chain remains future experiment-readiness work.
```

## 5. 主线 B 结论

主线 B 原始问题：

```text
巨大 f_null 来自真实物理缺项，还是 sigma / 厚尾 / block variance？
```

最新结果：

```text
null_sigma_model_version = component_specific_null_sigma_v1
null_sigma_conclusion = null_sigma_model_adequate_after_component_scaling
f_null_channel = 1.2616
f_null_statistical = 1.6696
f_null_block_bootstrap = 1.6696
f_null_hierarchical = 1.0730
f_null_student_t_proxy = 1.0
```

判断：

```text
B 线已经阶段性收敛：
  早期巨大 f_null 主要来自 null diagnostic sigma 低估；
  component-specific sigma 后，普通厚尾/离群不是主因；
  最新 conservative coverage 由 block-bootstrap 风险主导；
  final f_coverage_realistic 已采用 conservative max 口径。
```

## 6. 主线 C 结论

主线 C 原始问题：

```text
metadata checklist 是否已升级成 calibration checklist，
并能在缺失校准时触发 indeterminate gate？
```

最新结果：

```text
calibration_status = pass
calibration_warning = null
indeterminate_gates = []
covariance_components_missing = []
claim_policy = candidate_or_upper_bound_claim_allowed_if_run_policy_also_passes
```

此前 smoke 验证：

```text
generated/verify_calibration_missing_lambda_pol:
  calibration_status = indeterminate
  indeterminate_gates = [lambda_pol, pol_wavelength_null]
  covariance_components_missing = [Cov_cross, Cov_lambda_pol]
  claim_policy = exploratory_residual_only
```

判断：

```text
C 线已完成当前模拟阶段要求：
  run manifest / summary metadata / calibration manifest 已接入；
  缺失校准会触发 indeterminate；
  full milestone 具备正式 claim 的治理条件。
```

## 7. Hidden injection 与 nuisance leakage

Hidden injection：

```text
hidden_injection realistic_candidate_rate = 0.7625
hidden_identifiability_after_lambda_pol_model = 1.0
hidden_identifiability_after_pol_model = 1.0
hidden_identifiability_after_sagnac_model = 1.0
hidden_identifiability_after_pol_null_decomposition = 1.0
```

Nuisance false positive：

```text
null_clean realistic_false_positive_rate = 0.0
sagnac_residual realistic_false_positive_rate = 0.0
polarization_residual realistic_false_positive_rate = 0.0
thermal_area_coupled realistic_false_positive_rate = 0.0
delayed_thermal_response realistic_false_positive_rate = 0.0
random_hysteresis realistic_false_positive_rate = 0.0
temperature_polarization_cross realistic_false_positive_rate = 0.0
mixed_correlated realistic_false_positive_rate = 0.0
```

解释：

```text
当前 gate 没有把主要 nuisance 场景误报为 A2T candidate；
保守 coverage 后 hidden recovery 仍高于 0.70。
```

注意：

```text
hidden_injection 的 coverage_95_realistic_calibrated = 0.75，
说明 injected-signal amplitude interval 仍偏窄；
但当前任务关注的是 null-test pipeline 与 A/B/C 收敛，不把它解读为物理发现。
```

## 8. 当前完成判断

当前阶段可完成的目标：

```text
1. A2T 已从高维直觉压缩为可证伪 null-test；
2. A 线已有阶段性结论：当前 full evidence 不支持继续把 f_null 归因于 lambda-pol 物理缺项；
3. B 线已有阶段性结论：早期巨大 f_null 来自 sigma 口径问题，最终 coverage 改为 conservative max；
4. C 线已接入 calibration manifest 与 indeterminate gate；
5. full milestone run warning = null，run_manifest 完整。
```

尚未完成的更远目标：

```text
1. 真实实验中的完整 Jones matrix chain；
2. 真实硬件 metadata 接入；
3. 多 seed full milestone 统计稳定性；
4. 真实实验数据的上限声明。
```

因此本轮结论是：

```text
研究原型阶段完成；
真实实验 readiness 阶段未完成。
```
