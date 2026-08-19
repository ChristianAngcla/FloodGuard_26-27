# FLOODGUARD PRODUCTION SCREENSHOT & DEMO EVIDENCE INDEX

**Document ID:** `FLOODGUARD-DOC-SCREENSHOT-INDEX-20260820`  
**System:** FloodGuard Early Warning System (Marikina River Basin)  
**Classification:** Defense Demo & Visual Evidence Catalog  
**Capture Environment:** Live Production Firebase Hosting ([`https://floodguard-ai-6a9b6.web.app`](https://floodguard-ai-6a9b6.web.app)) & Flutter Mobile  
**Backend Host:** Remote Production ([`https://floodguard-api-xyjx.onrender.com`](https://floodguard-api-xyjx.onrender.com))  
**Date:** August 20, 2026  

---

## 1. Web Production Screenshots (`08_SCREENSHOTS_AND_DEMO/WEB/`)

| Filename | Screen / Route | Context | What It Proves | Important Values Visible | Recommended Defense Use |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`WEB_01_PUBLIC_OVERVIEW.png`** | `/admin` (Overview) | LIVE PRODUCTION | Live multi-station monitoring, telemetry summary, and interactive basin visualizer. | Sto. Niño, Tumana, Nangka live sensor levels. | Slide 1: System overview & real-time operation. |
| **`WEB_02_LIVE_VS_DAILY.png`** | `/admin/prediction` | LIVE PRODUCTION | Strict two-path architectural separation between live monitoring and next-day forecasting. | "CURRENT OBSERVED WATER LEVEL" vs "NEXT-CALENDAR-DAY DAILY FORECAST". | Slide 2: Two-path decoupling proof. |
| **`WEB_03_STO_NINO_FORECAST.png`** | `/admin/prediction` | LIVE PRODUCTION | Sto. Niño Candidate 9 evaluation, model metadata, and daily maximum water level target. | Candidate 9 (AR2 + BosoBoso lag-1), Target: Predicted Daily Maximum Water Level. | Slide 3: Sto. Niño MLR architecture. |
| **`WEB_04_NANGKA_FORECAST.png`** | `/admin/prediction` | LIVE PRODUCTION | Nangka Candidate 4 evaluation, station thresholds (16.50/17.10/17.70m). | Candidate 4 (AR1 + BosoBoso lag-1), Thresholds: Alert 16.50, Alarm 17.10, Critical 17.70m. | Slide 4: Nangka MLR architecture. |
| **`WEB_05_TUMANA_LIVE_VS_FORECAST.png`** | `/admin/prediction` | LIVE PRODUCTION | Tumana Candidate 8 evaluation, compatible thresholds (17.26/18.26/19.26m), and live emergency decoupling. | Candidate 8 (AR1 + Science Garden lag-1), Target: Predicted PAGASA-Reported Daily Water-Level Observation. | Slide 5: Tumana station & threshold proof. |
| **`WEB_06_FORECAST_UNAVAILABLE.png`** | `/admin/prediction` | LIVE PRODUCTION | Truthful null-handling: missing daily inputs render "Forecast unavailable", never "0.00 m" or fake "SAFE". | "Forecast unavailable" status, no fabricated numerical stage. | Defense Q&A: Proof of zero fake data or deceptive precision. |
| **`DEPLOY_01_FIREBASE_LIVE.png`** | Public Landing | LIVE PRODUCTION | Public production release deployed and active on Firebase Hosting. | URL: `https://floodguard-ai-6a9b6.web.app` | Slide 6: Production deployment proof. |

---

## 2. Admin Super-Admin Governance Screenshots (`08_SCREENSHOTS_AND_DEMO/ADMIN/`)

| Filename | Screen / Route | Context | What It Proves | Important Values Visible | Recommended Defense Use |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`ADMIN_01_CALIBRATION_OVERVIEW.png`** | `/TrainModel` | LIVE PRODUCTION | Final Phase 5 Controlled Recalibration engine (replaces legacy client training). | Active Models, Protected History, Exact Calendar Lags, Pure OLS. | Slide 7: Phase 5 statistical governance. |
| **`ADMIN_02_CALIBRATION_DIAGNOSTICS.png`** | `/TrainModel` | LIVE PRODUCTION | Comprehensive statistical diagnostic gates (OLS, HC3 SEs, VIF, persistence benchmark). | $R^2$, MAE, RMSE, HC3 p-values ($<0.05$), Max VIF ($<5.0$). | Slide 8: Statistical rigor & gate validation. |
| **`ADMIN_03_PASSWORD_RECONFIRMATION.png`** | `/TrainModel` | LIVE PRODUCTION | Two-person super-admin password reconfirmation required for production model deployment. | Password challenge dialog, role verification. | Slide 9: Operational safety & security controls. |
| **`ADMIN_04_AUDIT_ROLLBACK.png`** | `/TrainModel` | LIVE PRODUCTION | Immutable calibration audit history and zero-downtime rollback capability. | Version logs, timestamped actions, rollback triggers. | Slide 10: Traceability and disaster recovery. |

---

## 3. Flutter Mobile Screenshots (`08_SCREENSHOTS_AND_DEMO/MOBILE/`)

| Filename | Screen | Context | What It Proves | Important Values Visible | Recommended Defense Use |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`MOBILE_01_HOME_MAP.png`** | Home Screen | FLUTTER CLIENT | Responsive mobile map, sensor pins, and citizen alert status indicators. | Live basin map, alert level markers. | Mobile Demo 1: Citizen interface. |
| **`MOBILE_02_BARANGAY_DETAILS.png`** | Barangay Sheet | FLUTTER CLIENT | Decoupled display of live stage vs next-day forecast in mobile bottom sheet. | Live telemetry vs Daily forecast card. | Mobile Demo 2: Barangay-specific view. |
| **`MOBILE_03_STO_NINO.png`** | Station Card | FLUTTER CLIENT | Mobile representation of Sto. Niño Candidate 9 forecast. | Sto. Niño live stage & forecast. | Mobile Demo 3: Sto. Niño citizen advisory. |
| **`MOBILE_04_NANGKA.png`** | Station Card | FLUTTER CLIENT | Mobile representation of Nangka Candidate 4 forecast. | Nangka live stage & forecast. | Mobile Demo 4: Nangka citizen advisory. |
| **`MOBILE_05_TUMANA.png`** | Station Card | FLUTTER CLIENT | Mobile representation of Tumana Candidate 8 forecast & live threshold state. | Tumana live stage & forecast. | Mobile Demo 5: Tumana citizen advisory. |
| **`MOBILE_06_UNAVAILABLE.png`** | Station Card | FLUTTER CLIENT | Mobile client displays neutral unavailable state when sensor/forecast data is missing. | "Unavailable" badge, zero fake 0.00m. | Mobile Demo 6: Safe fail-closed handling. |

---

## 4. DOST-PAGASA Authoritative Source Telemetry Evidence (`01_RESEARCH_AND_DATA_PROOF/09_OPERATIONAL_PAGASA_THRESHOLD_AND_RAINFALL_EVIDENCE/`)

| Filename | Source | What It Proves | Authoritative Values Proved |
| :--- | :--- | :--- | :--- |
| **`TUMANA_STO_NINO_NANGKA_THRESHOLD_TABLE.png`** | DOST-PAGASA FFWS Portal | Official operational warning thresholds for Marikina River Basin stations. | **Tumana Bridge:** Alert: 17.26m, Alarm: 18.26m, Critical: 19.26m<br>**Sto. Niño:** Alert: 15.00m, Alarm: 16.00m, Critical: 17.00m<br>**Nangka:** Alert: 16.50m, Alarm: 17.10m, Critical: 17.70m |
| **`PAGASA_RAINFALL_BOSO_BOSO.png`** | DOST-PAGASA FFWS Portal | Boso-Boso rainfall station telemetry fields (`rf1hr` and `rfday`). | Cumulative rainfall inputs for Sto. Niño C9 and Nangka C4 models. |
| **`PAGASA_RAINFALL_SCIENCE_GARDEN.png`** | DOST-PAGASA Synoptic Station | Science Garden synoptic rainfall telemetry fields (`rf1hr` and `rfday`). | Cumulative rainfall input for Tumana C8 model. |
