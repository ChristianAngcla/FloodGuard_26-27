# FLOODGUARD MASTER PROOF CHAIN

This document traces the complete evidentiary chain from raw source data custody to operational system verification and live Firebase deployment.

```mermaid
graph TD
    A["Raw Historical Data Custody<br>(MMDA & DOST-PAGASA 2012–2025)"] --> B["Data Gate Audits & Cleaning<br>(Zero Imputation, Complete-Case)"]
    B --> C["Candidate Tournaments<br>(OLS MLR vs Persistence)"]
    C --> D["Certified Model Selection<br>(Sto C9, Nangka C4, Tumana C8)"]
    D --> E["Phase 1B: Server Models & Math Parity"]
    E --> F["Phase 2: 07:00 Daily Aggregation Pipeline"]
    F --> G["Phase 3: Deduplicated Daily FCM Dispatcher"]
    G --> H["Phase 4: Web & Mobile Two-Path UI Alignment"]
    H --> I["Phase 5: Recalibration & Statistical Governance"]
    I --> J["Tumana Operational Threshold Integration<br>(Alert 17.26m, Alarm 18.26m, Critical 19.26m)"]
    J --> K["UI & Forecast Integrity Fixes<br>(0.00 Null Bug Fixed, Projected Peak Removed)"]
    K --> L["Final System Verification<br>(95/95 Regression Tests PASS)"]
    L --> M["Live Firebase Deployment<br>(https://floodguard-ai-6a9b6.web.app)"]
```

## Proof Chain Milestones

1. **Raw Custody Proof:** `01_RESEARCH_AND_DATA_PROOF/01_SOURCE_AND_PROVENANCE/`
2. **Data Gate Proof:** `01_RESEARCH_AND_DATA_PROOF/02_DATA_AUDITS_AND_DATA_GATE/`
3. **Model Selection Proof:** `01_RESEARCH_AND_DATA_PROOF/04_CANDIDATE_MODEL_TOURNAMENTS/` & `06_FINAL_MODEL_SELECTION_PROOF/`
4. **PAGASA Operational Evidence:** `01_RESEARCH_AND_DATA_PROOF/09_OPERATIONAL_PAGASA_THRESHOLD_AND_RAINFALL_EVIDENCE/`
5. **Phase 1B–5 Implementation Proofs:** `02_PHASE_1B_SERVER_MODELS/` to `06_PHASE_5_CALIBRATION_GOVERNANCE/`
6. **Final System Verification (95/95 Tests):** `07_FINAL_SYSTEM_VERIFICATION/`
7. **Live Production Deployment:** `07_FINAL_SYSTEM_VERIFICATION/FLOODGUARD_FINAL_DEPLOYMENT_REPORT.md`
