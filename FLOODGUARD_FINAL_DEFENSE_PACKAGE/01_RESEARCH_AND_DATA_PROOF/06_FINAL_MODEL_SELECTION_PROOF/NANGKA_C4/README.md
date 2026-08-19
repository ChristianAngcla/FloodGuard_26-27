# Nangka Station — Candidate 4 Defense Dossier

- **Station ID:** `nangka`
- **Certified Model:** Candidate 4
- **Target Variable:** Daily Maximum Water Level (m)
- **Specification:** $\text{Nangka\_WL}_t = 8.1148 + 0.4898 \cdot \text{Nangka}_{t-1} + 0.0097 \cdot \text{BosoBoso}_{t-1}$
- **Key Metrics:**
  - Training N: 1,810 | Validation N: 318 | Final Refit N: 2,128
  - Validation MAE: `0.143768 m` | Validation RMSE: `0.384644 m`
  - Final Refit R²: `0.4335` | Max VIF: `1.5957`
  - HC3 Significance: All slopes statistically significant ($p < 0.001$).
- **Threshold Mapping Allowed:** `true` (Alert: 16.50m, Alarm: 17.10m, Critical: 17.70m)
- **Key Evidence:**
  - PDF: `FLOODGUARD_NANGKA_COMPLETE_DEFENSE_RECORD_R5_RECONCILED.pdf`
- **Selection & Benchmark Comparison:**
  - Candidate 4 ranked first and won **14 out of 14** exact-common pairwise MAE comparisons under the frozen validation rule.
  - Candidate 5 had a slightly lower validation RMSE (`0.380929 m` vs Candidate 4's `0.384644 m`), which is transparently disclosed.
  - On the same 318 validation dates, true persistence achieved MAE = `0.126774 m` and RMSE = `0.440142 m` (persistence had lower MAE; Candidate 4 had lower RMSE).
  - Event evidence was mixed: Candidate 4 performed best in Carina and rapid-rise subsets, but not every extreme subset.
