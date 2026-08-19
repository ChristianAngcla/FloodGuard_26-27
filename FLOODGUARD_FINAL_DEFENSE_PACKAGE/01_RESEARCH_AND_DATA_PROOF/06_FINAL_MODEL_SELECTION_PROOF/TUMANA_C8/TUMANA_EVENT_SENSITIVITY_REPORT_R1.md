# Tumana R3.1.2 Post-Selection Event-Sensitivity Audit (R1)

## Status and non-negotiable boundary

This is a **read-only sensitivity audit**. It does not change raw data, exact calendar lags, candidate definitions, OLS coefficients, HC3/VIF results, chronological-validation selection rule, Candidate 8 deployment equation, or runtime behavior.

The target remains exactly: **PAGASA-reported daily Tumana water-level observation**. It is not asserted to be a daily maximum, hourly peak, flood depth, flood probability, or official emergency trigger.

## Audit protocol locked before candidate comparison

- Evaluation period: the existing chronological validation period, 2022-05-27 through 2023-12-31.
- High-observation subset: reported daily Tumana observation >= **13.435 m**, the 90th percentile of non-missing *training* observations (2016-01-01 through 2022-05-26). This uses training data only to set the threshold.
- Rapid-rise subset: reported day-to-day increase >= **0.50 m**, based on exact calendar-day Tumana(t-1). This is a sensitivity threshold, not an official warning threshold.
- Critical union: either high observation or rapid rise.
- Metrics: MAE and RMSE; candidate-specific usable cases are shown. The principal C8-versus-C14 comparison is on their exact same usable dates.

## Results

| Subset | C8 (selected MLR) | C14 (eligible MLR alternative) | Finding |
|---|---|---|---|
| High reported daily observation | N=37, MAE=0.7581 m, RMSE=1.0649 m | N=37, MAE=0.6921 m, RMSE=0.9738 m | C14 lower MAE and RMSE |
| Rapid rise >= 0.50 m | N=22, MAE=0.8079 m, RMSE=1.1252 m | N=22, MAE=0.8031 m, RMSE=1.1129 m | C14 lower MAE and RMSE |
| High-or-rapid union | N=44, MAE=0.7023 m, RMSE=0.9960 m | N=44, MAE=0.6506 m, RMSE=0.9140 m | C14 lower MAE and RMSE |

## Correct conclusion

Candidate 14 performs better than Candidate 8 on these *post-selection validation sensitivity subsets*. This does **not** automatically make C14 the final deployed model because Candidate 8 was selected under a previously frozen, overall-validation MAE rule, while this audit was added afterward.

If FloodGuard now decides that high/rapid-rise performance is the primary operational objective, the defensible action is not a silent replacement. The team must write and apply one new, frozen event-aware decision rule to all three stations before comparing candidate results. That would be a new model-governance decision, not a repair of the old one.
