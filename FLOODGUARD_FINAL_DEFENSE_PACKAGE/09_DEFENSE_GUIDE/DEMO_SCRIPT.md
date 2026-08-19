# FLOODGUARD MASTER DEFENSE DEMONSTRATION SCRIPT

**Format:** 5–8 Minute Structured Defense Presentation & System Walkthrough  
**System:** FloodGuard Early Warning System (Marikina River Basin)  
**Target Audience:** Capstone Defense Panel & Technical Evaluators  

---

## 1. Introduction & Core Architecture (1 Minute)

> **Speaker:**  
> *"Good morning, esteemed panel members. FloodGuard is an early warning and decision-support system designed specifically for the Marikina River Basin.  
> Before diving into the live system, our most critical architectural principle is the **strict separation between two distinct operational paths**:"*

- **Path A — Real-Time Live Monitoring & Emergency Alerts:**  
  Consumes real-time DOST-PAGASA FFWS sensor telemetry. Citizen emergency push notifications and sirens trigger **strictly** when observed river levels cross operational alert, alarm, or critical stages upon state transitions.
- **Path B — Next-Calendar-Day MLR Forecasting:**  
  Evaluates certified, station-specific Ordinary Least Squares Multiple Linear Regression models (Candidate 9 for Sto. Niño, Candidate 4 for Nangka, and Candidate 8 for Tumana) using completed historical daily lags. This generates a **once-daily 07:00 AM PST planning advisory** for disaster managers without triggering false emergency evacuations.

---

## 2. Public Live Dashboard Walkthrough (1.5 Minutes)

> **Speaker:**  
> *(Show `WEB_01_PUBLIC_OVERVIEW.png` or live at `https://floodguard-ai-6a9b6.web.app`)*  
> *"Here on the public overview, disaster managers and citizens view real-time water levels across all three primary monitoring stations in the Marikina River Basin: Sto. Niño, Nangka, and Tumana Bridge.*  
> *Each station is calibrated to official DOST-PAGASA FFWS operational warning thresholds:"*

- **Sto. Niño:** Alert: `15.00m`, Alarm: `16.00m`, Critical: `17.00m`
- **Nangka:** Alert: `16.50m`, Alarm: `17.10m`, Critical: `17.70m`
- **Tumana Bridge:** Alert: `17.26m`, Alarm: `18.26m`, Critical: `19.26m` *(PAGASA FFWS Elevation Datum)*

---

## 3. Daily MLR Forecast & Two-Path Proof (2 Minutes)

> **Speaker:**  
> *(Navigate to `/admin/prediction` or show `WEB_02_LIVE_VS_DAILY.png`)*  
> *"On the prediction tool, you see the physical separation between Path A and Path B.*  
> *Notice that the current live telemetry reading is displayed on top, while the next-calendar-day daily forecast is displayed in its own dedicated card below.*  
> *Let's look at each certified station model:"*

1. **Sto. Niño (`WEB_03_STO_NINO_FORECAST.png`):**  
   Evaluates **Candidate 9** ($Y = eta_0 + eta_1 	ext{Sto}_{t-1} + eta_2 	ext{Sto}_{t-3} + eta_3 	ext{BosoBoso}_{t-1}$). Target: *Predicted Daily Maximum Water Level*.
2. **Nangka (`WEB_04_NANGKA_FORECAST.png`):**  
   Evaluates **Candidate 4** ($Y = eta_0 + eta_1 	ext{Nangka}_{t-1} + eta_2 	ext{BosoBoso}_{t-1}$). Target: *Predicted Daily Maximum Water Level*.
3. **Tumana Bridge (`WEB_05_TUMANA_LIVE_VS_FORECAST.png`):**  
   Evaluates **Candidate 8** ($Y = eta_0 + eta_1 	ext{Tumana}_{t-1} + eta_2 	ext{PAGASA\_SG\_Rain}_{t-1}$).  
   *Target Semantics:* Strict **PAGASA-reported daily Tumana water-level observation**.  
   *Threshold Mapping:* The next-day forecast is mapped against compatible station operational thresholds (`17.26` / `18.26` / `19.26m`) as an advisory forecast band. However, live emergency warnings remain strictly governed by observed telemetry.
4. **Fail-Closed Integrity (`WEB_06_FORECAST_UNAVAILABLE.png`):**  
   If input data is missing or incomplete, FloodGuard displays **"Forecast unavailable"**. It **never** defaults to `0.00 m` or fabricates a fake `SAFE` status.

---

## 4. Mobile Application & FCM Notifications (1 Minute)

> **Speaker:**  
> *(Show `MOBILE_01_HOME_MAP.png` and `MOBILE_02_BARANGAY_DETAILS.png`)*  
> *"On the Flutter mobile application, citizens receive clear, honest information without deceptive precision.*  
> *Firebase Cloud Messaging dispatches two separate notification types:"*

- **Live Emergency Alerts:** Dispatched immediately upon sensor stage transition to subscribed barangay topics (e.g. Tumana sends to `barangay_malanday`, `barangay_tumana`, `barangay_concepcion_uno`, `barangay_marikina_heights`, and `barangay_concepcion_dos`).
- **Daily Forecast Advisories:** Dispatched once per day at `07:00 AM PST` with deduplication protection.

---

## 5. Statistical Governance & Recalibration (1.5 Minutes)

> **Speaker:**  
> *(Navigate to `/TrainModel` or show `ADMIN_01_CALIBRATION_OVERVIEW.png` & `ADMIN_02_CALIBRATION_DIAGNOSTICS.png`)*  
> *"In Phase 5, we replaced all client-side training workflows with a strictly controlled Super-Admin Recalibration Engine:*
> 1. *Yearly raw dataset uploads are validated for schema and date continuity.*
> 2. *The system performs a protected historical merge with frozen 2016–2023 baseline data, rebuilding exact calendar lags across boundaries.*
> 3. *A pure OLS solver computes new regression parameters alongside HC3 heteroskedasticity-consistent standard errors and Variance Inflation Factors.*
> 4. *Statistical diagnostic gates verify significance ($p < 0.05$), non-collinearity ($	ext{VIF} < 5.0$), and persistence outperformance.*
> 5. *Production deployment requires super-admin password reconfirmation (`ADMIN_03_PASSWORD_RECONFIRMATION.png`), with full version history and instant rollback capability (`ADMIN_04_AUDIT_ROLLBACK.png`)."*

---

## 6. Verification & Conclusion (30 Seconds)

> **Speaker:**  
> *(Show `FLOODGUARD_FINAL_SYSTEM_VERIFICATION_REPORT.md` and live test execution)*  
> *"In conclusion, FloodGuard has passed 100% of its verification baseline: all **95 / 95 automated regression tests** passed, the web app is live on Firebase Hosting, the mobile APK is built, and the Master Defense Package is cryptographically sealed with SHA-256 integrity.*  
> *Thank you, and we welcome your questions."*
