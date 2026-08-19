# FLOODGUARD CERTIFIED MODELS QUICK REFERENCE

## 1. Station Summary & Equations

| Station | Candidate | Formula | Operational Warning Thresholds | Target Semantics |
| :--- | :--- | :--- | :--- | :--- |
| **Sto. Niño** | Candidate 9 | WL(t) = 3.545852 + 0.464200 * Sto(t-1) + 0.245693 * Sto(t-3) + 0.011525 * BosoBoso(t-1) | Alert: 15.00m<br>Alarm: 16.00m<br>Critical: 17.00m | Daily Maximum Water Level |
| **Nangka** | Candidate 4 | WL(t) = 8.114817 + 0.489769 * Nangka(t-1) + 0.009737 * BosoBoso(t-1) | Alert: 16.50m<br>Alarm: 17.10m<br>Critical: 17.70m | Daily Maximum Water Level |
| **Tumana** | Candidate 8 | WL(t) = 1.514724 + 0.873544 * Tumana(t-1) + 0.008482 * PAGASA_SG_Rain(t-1) | Alert: 17.26m<br>Alarm: 18.26m<br>Critical: 19.26m | PAGASA-reported daily observation |

## 2. Statistical Calibration & Diagnostics

| Station | Model | Train N | Val N | Refit N | Refit R² | Val MAE (m) | Val RMSE (m) | Max VIF |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Sto. Niño** | C9 | 1,969 | 472 | 2,441 | 0.8988 | 0.316347 | 0.591145 | 2.0610 |
| **Nangka** | C4 | 1,810 | 318 | 2,128 | 0.4335 | 0.143768 | 0.384644 | 1.5957 |
| **Tumana** | C8 | 1,068 | 580 | 1,648 | 0.8426 | 0.148147 | 0.324368 | 1.1212 |

## 3. Operational Architecture: Two-Path Separation
- **Path A (Live Emergency Monitoring):** Actual real-time sensor reading vs station thresholds -> Live Status -> Live FCM Alerts.
- **Path B (Daily Decision-Support Forecasting):** Certified MLR equation on completed calendar lags -> Next-Day Predicted Water Level -> Forecast Advisory Band.
