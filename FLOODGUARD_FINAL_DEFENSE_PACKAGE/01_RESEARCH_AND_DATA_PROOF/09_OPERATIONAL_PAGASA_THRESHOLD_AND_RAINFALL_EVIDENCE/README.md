# DOST-PAGASA OPERATIONAL THRESHOLD AND RAINFALL TELEMETRY EVIDENCE

**Document ID:** `FLOODGUARD-EVIDENCE-PAGASA-OPERATIONAL-20260820`  
**Source Authority:** DOST-PAGASA Flood Forecasting and Warning System (FFWS) for the Pasig-Marikina-Tullahan River Basin  
**Classification:** Authoritative Operational Source Evidence Archive  
**Date Confirmed:** August 20, 2026  

---

## 1. Official Operational Water-Level Warning Thresholds

The official DOST-PAGASA FFWS operational telemetry displays current water levels alongside the authoritative station warning threshold table:

| Station Name | Alert Level | Alarm Level | Critical Level | Datum / Unit |
| :--- | :---: | :---: | :---: | :---: |
| **Sto. Niño Monitoring Station** | 15.00 m | 16.00 m | 17.00 m | Elevation in meters (EL.m) |
| **Nangka River Station** | 16.50 m | 17.10 m | 17.70 m | Elevation in meters (EL.m) |
| **Tumana Bridge Station** | 17.26 m | 18.26 m | 19.26 m | Elevation in meters (EL.m) |

Evidence Artifact: `TUMANA_STO_NINO_NANGKA_THRESHOLD_TABLE.png`

---

## 2. Operational Response Level Semantics

- **Normal / Safe:** River elevation below Alert threshold.
- **ALERT:** Water level reaches the Alert stage; heightened monitoring and community awareness.
- **ALARM:** Water level reaches the Alarm stage; preparedness for low-lying areas.
- **CRITICAL:** Observed water level has reached or exceeded the official Critical threshold.
  - *Note:* Emergency actions and evacuation measures remain subject to official PAGASA, LGU, and MDRRMO protocols and advisories.

---

## 3. Real-Time Upstream Rainfall Telemetry Screens

The official DOST-PAGASA FFWS telemetry interface presents two distinct rainfall metrics for monitoring stations:
1. **RF [mm] 1-Hour:** Instantaneous hourly rainfall accumulation.
2. **RF [mm] Daily Sum (24hr):** Rolling 24-hour total rainfall accumulation.

### Station Mapping & Model Dependencies
- **Boso Boso (Mt. Boso-Boso Station):**
  - Upstream rainfall predictor for **Sto. Niño (Candidate 9)** and **Nangka (Candidate 4)**.
  - Evidence Artifact: `PAGASA_RAINFALL_BOSO_BOSO.png`
- **Science Garden (PAGASA Science Garden Station):**
  - Rainfall predictor for **Tumana Bridge (Candidate 8)**.
  - Evidence Artifact: `PAGASA_RAINFALL_SCIENCE_GARDEN.png`

---

## 4. Strict Model Construction & Two-Path Segregation

1. **Daily Model Inputs:** Certified daily models strictly use the completed prior calendar-day rainfall variables constructed under Phase 2 strict daily aggregation contracts. The live displayed 24-hour rolling sum is operational telemetry evidence and does not bypass the certified daily pipeline.
2. **Tumana Bridge Model Target Semantics:** Candidate 8 model target remains strictly **"PAGASA-reported daily Tumana water-level observation"**. No assumptions or inferences regarding intraday timing (e.g. 8 AM vs midnight vs peak) are made.
3. **Two-Path Architecture:**
   - **Path A (Live Emergency Monitoring):** Actual live telemetry is compared in real-time against official thresholds (Sto: 15/16/17m, Nangka: 16.5/17.1/17.7m, Tumana: 17.26/18.26/19.26m) to generate real-time emergency push notifications upon state transition/escalation.
   - **Path B (Daily Decision-Support Forecasting):** Certified MLR models predict next-calendar-day water levels, mapped into forecast advisory bands for decision support (`thresholdMappingAllowed: true`). Daily forecasts **never** trigger live emergency evacuation sirens or alerts.
