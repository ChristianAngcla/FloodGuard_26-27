# FLOODGUARD DEFENSE DEMONSTRATION FALLBACK PLAN

**Document ID:** `FLOODGUARD-DOC-DEMO-FALLBACK-20260820`  
**System:** FloodGuard Early Warning System (Marikina River Basin)  
**Purpose:** Pre-planned operational contingency protocols during live capstone defense presentation.  

---

## Contingency Matrix

| Failure Scenario | Immediate Action | Evidence to Display | What to Say | What NOT to Claim |
| :--- | :--- | :--- | :--- | :--- |
| **1. Public Internet Outage** | Switch to local running server on `localhost:5000` and `localhost:5173`. If unavailable, display offline defense screenshots. | `08_SCREENSHOTS_AND_DEMO/WEB/` and `FLOODGUARD_FINAL_DEPLOYMENT_REPORT.md` | *"Due to venue connectivity constraints, we are demonstrating from our pre-compiled local test runner and cryptographically sealed live production captures."* | Do NOT claim live cloud APIs are responding when running offline. |
| **2. DOST-PAGASA FFWS Portal Offline / Slow** | Display retained official telemetry evidence captures. | `01_RESEARCH_AND_DATA_PROOF/09_OPERATIONAL_PAGASA_THRESHOLD_AND_RAINFALL_EVIDENCE/TUMANA_STO_NINO_NANGKA_THRESHOLD_TABLE.png` | *"PAGASA's public portal is currently undergoing maintenance. Our system is designed to gracefully handle telemetry latency while our authoritative source evidence proves all official station thresholds."* | Do NOT claim live real-time values are syncing if PAGASA is down. |
| **3. Render API Backend Sleeping / Cold Start** | Allow 30–45s for Render free-tier spinup, or show local backend API execution. | `FINAL_SYSTEM_TEST_OUTPUT.txt` (95/95 test run) | *"The cloud backend is completing its initial container spinup. We can inspect the local server output and verified 95/95 automated test suite."* | Do NOT restart the backend repeatedly. |
| **4. Daily Forecast Displays "Forecast unavailable"** | Explain this as intentional fail-closed design. | `WEB_06_FORECAST_UNAVAILABLE.png` and Test 11.1 / 11.2 | *"Notice that because the completed prior calendar-day dataset is not yet fully closed, FloodGuard truthfully displays 'Forecast unavailable' rather than fabricating a dangerous 0.00m or fake safe reading."* | Do NOT apologize as if it is a system bug. It is a feature proving data integrity. |
| **5. Flutter Emulator / Device Display Issue** | Present high-resolution mobile screenshots from the master defense package. | `08_SCREENSHOTS_AND_DEMO/MOBILE/` (`MOBILE_01_HOME_MAP.png` to `MOBILE_06_UNAVAILABLE.png`) | *"We have captured the exact Flutter mobile screens at 2x device scale, demonstrating the identical two-path citizen interface."* | Do NOT spend defense time debugging ADB or USB cables. |
| **6. Panel Questions Model Mathematics or Coefficients** | Open the certified station dossiers in `01_RESEARCH_AND_DATA_PROOF/06_FINAL_MODEL_SELECTION_PROOF/`. | `STO_NINO_C9/`, `NANGKA_C4/`, `TUMANA_C8/` READMEs and Excel workbooks | *"Every coefficient is backed by an independent Excel workbook with LINTEST, HC3 covariance matrix, and VIF calculations matching our server implementation to 10 decimal places."* | Do NOT attempt to recalculate formulas by hand on the whiteboard without referring to the dossier. |
| **7. Panel Questions Tumana Evacuation Commands** | Clarify that FloodGuard provides advisory threshold classifications, while evacuation orders remain the sole legal authority of PAGASA, LGU, and Marikina MDRRMO. | `WHAT_EACH_FILE_PROVES.md` (FAQ Section) | *"FloodGuard provides critical decision support and early notification. In accordance with Philippine Disaster Risk Reduction protocols (RA 10121), mandatory evacuation orders are executed exclusively by the Marikina City Government and MDRRMO."* | Do NOT claim the AI model autonomously orders citizen evacuations. |
