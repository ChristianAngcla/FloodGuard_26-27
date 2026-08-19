# FLOODGUARD PHASE 5 — CONTROLLED SUPER-ADMIN IN-SYSTEM RECALIBRATION & STATISTICAL GOVERNANCE REPORT (FINAL SEALED)

**Document ID:** FLOODGUARD-DOC-PHASE5-CALIBRATION-GOVERNANCE-20260819-FINAL  
**Author:** Antigravity (Advanced Agentic Architecture)  
**System:** FloodGuard Flood Early Warning System (Marikina River Basin)  
**Status:** ✅ **PHASE 5 PERMANENTLY SEALED — READY FOR FINAL SYSTEM VERIFICATION**  
**Date:** August 19, 2026  

---

## 1. Executive Summary

Phase 5 implements the complete, production-hardened statistical recalibration, governance, and model lifecycle subsystem for FloodGuard. The platform enables authorized Super-Administrators to upload new calendar-year telemetry datasets (CSV/XLSX), rigorously preprocess and lag-reconstruct historical time-series, evaluate candidates using chronological train/validation splits, fit production models with pure Ordinary Least Squares (OLS), calculate Heteroskedasticity-Consistent (HC3) robust standard errors, assess Variance Inflation Factors (VIF), and deploy updated model coefficients with password reconfirmation and automated single-click rollback.

### Key Governance Guarantees
1. **Canonical Internal Normalized Raw Schema**: All raw rows from every source (protected CSV, prior accepted snapshots, and current upload) normalize per-row to { Date: 'YYYY-MM-DD', waterLevel: number | null, rainfall: number | null } before cutoff calculation, cumulative merge, and lag reconstruction.
2. **Cumulative Historical Merge**: Incorporates static 2016–2023 protected baselines + all prior accepted yearly snapshots (DEPLOYED/SUPERSEDED) + new valid upload data.
3. **Exact Calendar Lag Reconstruction**: Reconstructs exact calendar lags (-1 = \text{Date}-1\text{d}$, -3 = \text{Date}-3\text{d}$) dynamically across annual and cross-snapshot boundaries. Precomputed lag columns in archives are ignored.
4. **Complete-Case Analysis**: Missing or unresolvable measurement rows remain strictly 
ull (no zero-filling, no forward-filling, no interpolation). Incomplete lag rows are dropped from the OLS regression matrix.
5. **Pure OLS & HC3 Inference**: Model coefficients are estimated via closed-form OLS ^{-1} X^T y$ without regularization. HC3 robust standard errors and $-values provide statistical governance without altering point predictions.
6. **Collinearity Governance (VIF)**: Collinearity is audited via VIF ( / (1 - R_j^2)$). A maximum VIF $\le 5.0$ gate prevents activation of multicollinear models.
7. **Two-Stage Workflow**: Stage A (80/20 chronological train/val split) computes out-of-sample evaluation metrics; Stage B (100% complete-case historical refit) produces activatable production coefficients.
8. **Strict Authentication & Security**: Super-admin role verification via JWT, password reconfirmation for activation/rollback, no client-submitted coefficients, zero hardcoded JWT fallback, and quarantined legacy training endpoints.

---

## 2. Canonical Internal Raw Schema & Accepted External Aliases

### Canonical Internal Schema (Post-Normalization)
`	ypescript
interface CanonicalRawDailyRecord {
    Date: string;               // ISO 'YYYY-MM-DD' calendar date
    waterLevel: number | null;  // Float in meters (null if missing/blank; 0.0 preserved)
    rainfall: number | null;    // Float in millimeters (null if missing/blank; 0.0 preserved)
}
`

### Accepted External Column Aliases per Station

| Station ID | Candidate Specification | Accepted Date Aliases | Accepted In-Situ Water Level Aliases | Accepted Upstream Rainfall Aliases |
| :--- | :--- | :--- | :--- | :--- |
| **sto_nino** | Candidate 9 (Sto_t_1, Sto_t_3, BosoBoso_t_1) | Date, date, 	imestamp, Timestamp | Sto, Sto_Nino_WL_max, Sto_Nino_WL, Sto_WL | BosoBoso, Mt_BosoBoso, Mt_Bosoboso, BosoBoso_Rain, osoboso_rfday |
| **
angka** | Candidate 4 (
angka_wl_t_1, osoboso_rain_t_1) | Date, date, 	imestamp, Timestamp | Nangka_WL_max, Nangka_WL, NangkaWL, Nangka | Mt_BosoBoso, Mt_Bosoboso, BosoBoso, BosoBoso_Rain, osoboso_rfday |
| **	umana** | Candidate 8 (	umana_wl_t_1, pagasa_sg_rain_t_1) | Date, date, 	imestamp, Timestamp | Tumana_WL, Tumana, 	umana_wl | PAGASA_SG_Rain, ScienceGarden, Science_Garden, ScienceGarden_Rain, pagasa_sg_rain, 
fday |

* **Normalization Timing**: Normalization occurs in memory via 
ormalizeRawDailyRow(stationId, row) immediately upon loading prior snapshots and current uploads, before cutoff calculation, merge, sorting, or lag rebuilding.
* **HTTP Route Cutoff**: In calibrationRoutes.js, prior DEPLOYED/SUPERSEDED calibration rows are individually normalized to extract their canonical .Date, guaranteeing accurate latestAcceptedDate cutoff detection regardless of header differences between prior years and the current upload.

---

## 3. Cryptographically Protected Historical Datasets

The static 2016–2023 protected baseline CSV files remain strictly immutable on disk and are verified via SHA-256 upon every load:

| Station | Protected Baseline CSV | Row Count | SHA-256 Checksum |
| :--- | :--- | :--- | :--- |
| **Sto. Niño** | sto_nino_protected_history.csv | 2,922 rows | 187867e762744f871279d4bad2da9fc1f1c7ff76cbc2fe65ea4cb41ed2be6de5 |
| **Nangka** | 
angka_protected_history.csv | 2,922 rows | 678ef76f8f447fed3500fe379aedfa087157dbadc9da62311bf3f95ade6137c7 |
| **Tumana** | 	umana_protected_history.csv | 2,922 rows | 8984cd500c285a6201c07315b7a5a6ad9c08f31fb06d6bc37f5510dbfa02473 |

---

## 4. Certified Canonical Reproduction Parity Results

Parity is validated by running 
unCalibration with isCanonicalFixture = true on the canonical fixture CSVs and verifying parameter divergence against certified baseline models:

\max_j |\beta_j^{\text{computed}} - \beta_j^{\text{certified}}| \le 1 \times 10^{-5}

| Station | Candidate | Sample Size ($) | Certified Coefficients | Max Absolute Difference | Parity Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Sto. Niño** | Candidate 9 |  = 2,441$ | $\beta_0 = 3.545852$<br>$\beta_{\text{Sto}_{t-1}} = 0.464200$<br>$\beta_{\text{Sto}_{t-3}} = 0.245693$<br>$\beta_{\text{BosoBoso}_{t-1}} = 0.011525$ | **.70 \times 10^{-12}$** | ✅ **PASS** |
| **Nangka** | Candidate 4 |  = 2,128$ | $\beta_0 = 8.114817$<br>$\beta_{\text{Nangka}_{t-1}} = 0.489769$<br>$\beta_{\text{BosoBoso}_{t-1}} = 0.009737$ | **.04 \times 10^{-10}$** | ✅ **PASS** |
| **Tumana** | Candidate 8 |  = 1,648$ | $\beta_0 = 1.514724$<br>$\beta_{\text{Tumana}_{t-1}} = 0.873544$<br>$\beta_{\text{ScienceGarden}_{t-1}} = 0.008482$ | **.41 \times 10^{-12}$** | ✅ **PASS** |

---

## 5. Complete Verification Test Suite Breakdown (81 / 81 Tests PASS)

`	ext
================================================================
FLOODGUARD PHASE 3 FINAL DELIVERY-SEALED VERIFICATION SUITE
================================================================

[PASS] 1.1 Sto. Niño C9 Parity (Normal Operation)
[PASS] 1.2 Sto. Niño C9 Persistence Fallback (Missing Rain)
[PASS] 2.1 Nangka C4 Parity (Normal Operation)
[PASS] 2.2 Nangka C4 Persistence Fallback (Missing Rain)
[PASS] 3.1 Tumana C8 Parity (Normal Operation)
[PASS] 3.2 Tumana C8 Persistence Fallback (Missing Science Garden Rain)
[PASS] 3.3 Tumana Target Semantics & Strict Unmapped Restrictions
[PASS] 4.1 [Phase 2] Separate Water & Rain Source Timestamps Across Midnight Boundary
[PASS] 4.2 [Phase 2] Strict 24/24 Hourly Completeness (Sto & Nangka)
[PASS] 6.1 Sto. Niño primary_model Message Format
[PASS] 6.2 Nangka primary_model Message Format
[PASS] 6.3 Persistence Fallback Message Text
[PASS] 6.4 Tumana Message Semantics (Zero Threshold / Peak / Probability Wording)
[PASS] 6.5 Tumana Unavailable Forecast Sends Nothing (Null Message)
[PASS] 6.6 Sto/Nangka Unavailable Forecast Sends Nothing (Null Message)
[PASS] 6.7 [Required Test A] Firebase Unavailable Marks Record Failed (Never Sent)
[PASS] 6.8 [Required Test B] All Topic Sends Fail Marks Record Failed (Eligible for Retry)
[PASS] 6.9 [Required Test C] Successful Delivery Marks Record Sent with Timestamp
[PASS] 6.10 [Required Test D] Deduplicated Second Run Skips Dispatching
[PASS] 6.11 [Required Test E] Atomic Concurrent Claim Prevents Race Conditions
[PASS] 6.12 [Required Test F] Canonical Barangay Topic Consistency Across All Server Paths
[PASS] 6.13 [Check I] Five-Minute Background Telemetry Sync Does NOT Trigger FCM
[PASS] 6.14 [Check J] Manual triggerManualForecastRun Defaults sendNotifications = false
[PASS] 6.15 [Check K] Daily Notification Consumes Persisted DailyForecast, Not Live Sensors
[PASS] 6.16 [Check L] Manual Admin Alert Endpoint Exists and Uses Canonical Topic Format
[PASS] 7.1 Zero rejectUnauthorized: false Across Server Code
[PASS] 7.2 Schema Validation for DailyForecast Deduplication & Sending Fields
[PASS] 7.3 Server Critical Files Parse Successfully (node --check)

================================================================
PHASE 5: CONTROLLED SUPER-ADMIN RECALIBRATION & GOVERNANCE
================================================================

[PASS] 8.1 [Required Test 12] Zero Occurrences of Hardcoded JWT Secret Fallback
[PASS] 8.2 [Required Test 13] Missing JWT_SECRET Fails Closed Immediately
[PASS] 8.3 [Security Test A] Unauthenticated Calibration Access is Rejected (401)
[PASS] 8.4 [Security Test B] Regular Admin User Cannot Mutate Calibrations (403)
[PASS] 8.5 [Security Test C] Super-Admin Role Successfully Passes Super-Admin Guard
[PASS] 8.6 [Security Test D] Activation Requires Super-Admin Password Reconfirmation
[PASS] 8.7 [Security Test E] Rollback Requires Super-Admin Password Reconfirmation
[PASS] 8.8 [Security Test F] Client-Submitted Custom Beta Coefficients are Prohibited
[PASS] 8.9 [Security Test G] Quarantined Legacy Training Endpoints Return 410 Gone
[PASS] 8.10 [Security Test H] Passwords and Hashes Never Stored in Calibration Records or Audit Logs
[PASS] 9.1 [Required Test 1] Historical Merge Combines Protected & New Yearly Rows Chronologically
[PASS] 9.2 [Required Test 2] Cross-Year Exact Lag Arithmetic Across Calendar Boundary
[PASS] 9.3 [Required Test 3] Overlap with Protected History is Strictly Rejected
[PASS] 9.4 [Required Test 4] Duplicate Upload Dates Inside Upload are Strictly Rejected
[PASS] 9.5 [Required Test 5] Invalid and Future Dates are Strictly Rejected
[PASS] 9.6 [Required Test 6] Source Survives Server Restart Semantics (Durable Snapshot)
[PASS] 9.7 [Required Test 7] Client Body Row Replacement is Prohibited on /run
[PASS] 9.8 [Required Test 8] Chronological Evaluation Subset vs Full-History Final Refit
[PASS] 9.9 [Required Test 9] Activation Deploys Final Refit Coefficients (Not Evaluation Subset)
[PASS] 9.10 [Required Test 10] Canonical Reproduction Fixture Parity (<= 1e-5 for Sto, Nangka, Tumana)
[PASS] 9.11 [Required Test 11] Future Year Recalibration Does NOT Require Old Beta Equality
[PASS] 9.12 [Required Test A] Real Protected CSV + Raw 2024 Daily Data for Sto. Niño
[PASS] 9.13 [Required Test B] Real Protected CSV + Raw 2024 Daily Data for Nangka
[PASS] 9.14 [Required Test C] Real Protected CSV + Raw 2024 Daily Data for Tumana
[PASS] 9.15 [Required Test D] Extreme New Year Data Changes Final OLS Refit
[PASS] 9.16 [Required Test E] Cross-Year Exact Lags Built from Raw Observations with Actual Protected File
[PASS] 9.17 [Required Test F] Second-Year Cumulative History (2016–2023 + DEPLOYED 2024 + Current 2025)
[PASS] 9.18 [Required Test G] Prior Accepted Year Snapshot Resolves Cross-Year Lags
[PASS] 9.19 [Required Test H] Overlap with Prior Accepted Year is Strictly Rejected
[PASS] 9.20 [Required Test I] Canonical Fixture Flag Cannot Be Set by HTTP Upload
[PASS] 9.21 [Required Test J] Fixture Records Cannot Be Activated for Production
[PASS] 9.22 [Required Test K] Strict Yearly Raw-Schema Validation and Malformed Text Rejection
[PASS] 9.23 [Alias Test A] Sto Alternate Target/Rain Aliases Contribute Full History
[PASS] 9.24 [Alias Test B] Sto Lowercase Date Alias — Full History Preserved
[PASS] 9.25 [Alias Test C] Nangka Alias Mix — Historical + Yearly Both Contribute
[PASS] 9.26 [Alias Test D] Tumana Alias Mix — Historical + Yearly Both Contribute (Strictly Unmapped)
[PASS] 9.27 [Alias Test E] Prior Year with Different Aliases — Three-Source Cumulative History
[PASS] 9.28 [Alias Test F] Overlap Detection Works Across Different Date Aliases
[PASS] 9.29 [Alias Test G] Canonical Headers Still Produce Correct Results
[PASS] 9.30 [Alias Test H] Canonical Parity After Normalization (All Three Stations <= 1e-5)
[PASS] 9.31 [Route Test A] HTTP Upload Route Cutoff Normalization Rejects Overlapping Date with Heterogeneous Aliases
[PASS] 9.32 [Route Test B] HTTP Upload Route Cutoff Normalization Accepts Valid Successive Year
[PASS] 10.1 Pure OLS Solver Correctness on Synthetic Matrix
[PASS] 10.2 Singular / Rank-Deficient Matrix Rejection
[PASS] 10.3 Heteroskedasticity-Consistent HC3 Covariance Standard Errors
[PASS] 10.4 HC3 Inference Strictly Does NOT Alter Point Predictions
[PASS] 10.5 VIF Collinearity Diagnostics Functionality
[PASS] 10.6 Complete-Case Rule (Missing Rows Dropped, Never Filled)
[PASS] 10.7 Diagnostic Failure Blocks Approval and Activation
[PASS] 10.8 Cryptographic Verification of Protected Historical Datasets on Load
[PASS] 10.9 Dynamic Active Model Version Resolver Fallback Safety
[PASS] 10.10 Custom Deployed Version Evaluation in DailyForecastService
[PASS] 10.11 Immutable Audit Log Schema and Action Tracking

================================================================
TEST SUMMARY: 81/81 PASSED (100%)
================================================================
ALL PHASE 1B, 2, 3, 4, AND 5 TESTS PASSED SUCCESSFULLY.
`

### Test Suite Distribution
- **Phases 1B / 2 / 3 / 4 (Tests 1.1 – 7.3)**: 28 tests
- **Phase 5 Security & Governance (Tests 8.1 – 8.10)**: 10 tests
- **Phase 5 Historical Merge & Recalibration (Tests 9.1 – 9.22)**: 22 tests
- **Phase 5 Column-Alias Normalization (Tests 9.23 – 9.30)**: 8 tests
- **Phase 5 HTTP Upload Route Cutoff Normalization (Tests 9.31 – 9.32)**: 2 tests
- **Phase 5 Statistical OLS, HC3, VIF & Diagnostics (Tests 10.1 – 10.11)**: 11 tests
- **Total**: **81 / 81 PASSED (100%)**

---

## 6. Build and Syntax Verification

* **Node.js Syntax Checks (
ode --check)**:
  - server/routes/calibrationRoutes.js → Syntax OK
  - server/services/calibrationEngine.js → Syntax OK
  - server/index.js → Syntax OK
* **Frontend Web Production Build (
pm run build)**: Vite 7.3.2 production build completed in **6.65s** with 0 errors.

---

## 7. Sealed Phase 5 Artifact Deliverables

1. **Governance Report**: FLOODGUARD_PHASE_5_CALIBRATION_GOVERNANCE_REPORT.md
2. **Test Output Log**: PHASE_5_CALIBRATION_TEST_OUTPUT.txt
3. **Review Bundle ZIP**: FLOODGUARD_PHASE_5_CALIBRATION_REVIEW_BUNDLE.zip
4. **Bundle Checksum**: FLOODGUARD_PHASE_5_CALIBRATION_REVIEW_BUNDLE_CHECKSUM.txt

---

**PHASE 5 PERMANENTLY SEALED — READY FOR FINAL SYSTEM VERIFICATION**
