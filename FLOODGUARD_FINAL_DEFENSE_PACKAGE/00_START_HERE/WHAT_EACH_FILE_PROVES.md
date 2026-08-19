# WHAT EACH PROOF FILE PROVES

### 1. Research & Model Selection Proofs (01_RESEARCH_AND_DATA_PROOF/)
- **01_SOURCE_AND_PROVENANCE/:** Proves raw data custody from MMDA and DOST-PAGASA (2012–2025).
- **02_DATA_AUDITS_AND_DATA_GATE/:** Proves sample completeness, data cleaning gates, and zero imputation on missing values.
- **04_CANDIDATE_MODEL_TOURNAMENTS/:** Proves pre-registered tournament model evaluation across all candidate architectures.
- **05_OLS_MLR_STATISTICAL_PROOF/:** Proves OLS MLR statistical validity, HC3 robust standard errors (p < 0.001), and low multicollinearity (VIF < 2.1).
- **06_FINAL_MODEL_SELECTION_PROOF/:** Complete dossiers for Sto. Niño C9, Nangka C4, and Tumana C8.
- **09_OPERATIONAL_PAGASA_THRESHOLD_AND_RAINFALL_EVIDENCE/:** Proves official PAGASA FFWS warning thresholds (Sto. Niño: 15/16/17m, Nangka: 16.5/17.1/17.7m, Tumana: 17.26/18.26/19.26m) and telemetry rainfall monitoring screens.

### 2. System Implementation Proofs (02_PHASE_1B_SERVER_MODELS/ to 06_PHASE_5_CALIBRATION_GOVERNANCE/)
- Proves end-to-end operational software implementation: frozen model evaluation, 07:00 daily automated pipeline, deduplicated daily FCM advisories, Web & Flutter UI, and super-admin recalibration.

### 3. Final System Verification & Deployment Proofs (07_FINAL_SYSTEM_VERIFICATION/)
- **FLOODGUARD_FINAL_SYSTEM_VERIFICATION_REPORT.md:** Proves 95/95 test execution, static syntax validation, Web and Admin production builds, Flutter analyze (0 issues), and debug APK build.
- **FINAL_SYSTEM_TEST_OUTPUT.txt:** Raw unedited console execution output of the 95/95 server regression suite.
- **FLOODGUARD_FINAL_DEPLOYMENT_REPORT.md:** Proves live Firebase Hosting deployment (`https://floodguard-ai-6a9b6.web.app`), remote Render backend connectivity, and 0.00 forecast bug elimination.
- **POST_TUMANA_OPERATIONAL_CORRECTION_README.md:** Audit traceability explaining the evolution of operational threshold handling.

---

## Defense FAQ & Evidence Pointers

### Q1: Where is proof that Tumana Bridge has official thresholds?
**Answer:** In `01_RESEARCH_AND_DATA_PROOF/09_OPERATIONAL_PAGASA_THRESHOLD_AND_RAINFALL_EVIDENCE/`, which contains the official DOST-PAGASA FFWS operational telemetry screen capture (`TUMANA_STO_NINO_NANGKA_THRESHOLD_TABLE.png`) proving Alert: 17.26 EL.m, Alarm: 18.26 EL.m, and Critical: 19.26 EL.m.

### Q2: How do you prove Tumana live alerts do not come from daily forecasts?
**Answer:** In `07_FINAL_SYSTEM_VERIFICATION/`, specifically automated server tests 3.9 and 3.10:
- Test 3.9 proves that when daily forecast is Critical (19.50m) while live observed telemetry is Safe (14.00m), live status remains SAFE and zero emergency FCM alerts are dispatched.
- Test 3.10 proves that when live observed telemetry is Critical (19.50m) while daily forecast is Safe (12.50m), live emergency FCM alerts are dispatched immediately based solely on live telemetry.

### Q3: Which barangays receive Tumana emergency notifications?
**Answer:** Malanday, Tumana, Concepcion Uno, Marikina Heights, and Concepcion Dos.
- Formatted topics: `barangay_malanday`, `barangay_tumana`, `barangay_concepcion_uno`, `barangay_marikina_heights`, `barangay_concepcion_dos`.
- Proved in `07_FINAL_SYSTEM_VERIFICATION/` (Test 3.12).

### Q4: How is missing daily forecast data displayed to users?
**Answer:** As `"Forecast unavailable"` (Test 11.1 & Test 11.2). Missing data is never coerced to `0.00 m` or defaulted to `SAFE`.
