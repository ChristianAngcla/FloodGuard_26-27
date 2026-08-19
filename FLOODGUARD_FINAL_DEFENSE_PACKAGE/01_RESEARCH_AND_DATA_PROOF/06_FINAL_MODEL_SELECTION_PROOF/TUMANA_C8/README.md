# Tumana Bridge — Candidate 8 Frozen Model Dossier

## Model Equation (Certified Production)
Tumana_WL(t) = 1.5147240224821763 + 0.8735442115350864 * Tumana_WL(t-1) + 0.008481630145296813 * PAGASA_SG_Rain(t-1)

## Dependent Variable Target Semantics
- **Target:** PAGASA-reported daily Tumana water-level observation (Tumana_WL, unit: meters EL.m).
- **Target Semantics:** STRICTLY "PAGASA-reported daily Tumana water-level observation". It is not a 24-hour peak or daily maximum, reflecting the empirical reporting interval of the primary source gauge.

## Official Operational Thresholds (PAGASA FFWS)
- **Alert:** `17.26 EL.m`
- **Alarm:** `18.26 EL.m`
- **Critical:** `19.26 EL.m`
- **Live Monitoring (Path A):** Live telemetry is compared against 17.26 / 18.26 / 19.26 m to generate real-time emergency warnings and FCM alerts.
- **Daily Forecast (Path B):** Next-calendar-day predictions map to threshold bands as decision-support advisories (thresholdMappingAllowed: true).

## Statistical Diagnostics & Candidate Tournament
- **Training Period:** 2016-01-01 to 2020-12-31 (N = 1,068)
- **Validation Period:** 2021-01-01 to 2023-12-31 (N = 580)
- **Full Refit Sample:** N = 1,648, Refit R² = 0.842641
- **Validation Metrics:**
  - Candidate 8: MAE = 0.148147 m, RMSE = 0.324368 m, Max VIF = 1.1212
  - True Persistence (Lag-1): MAE = 0.1416 m, RMSE = 0.3604 m
  - Candidate 14: MAE = 0.1514 m, RMSE = 0.3101 m
- **Operational Fallback:** When lag-1 Science Garden rainfall is missing, the system gracefully falls back to true lag-1 water level persistence (0.8735 * WL + 1.51 -> Persistence).
