# Honest Project Limitations & Operational Boundaries

FloodGuard maintains complete scientific and engineering transparency regarding system boundaries.

1. **Daily Resolution vs. Intraday Hydrographs:** Certified models operate on a daily timestep (projecting daily maximum water level for Sto. Niño/Nangka and daily observation for Tumana). They are designed for day-ahead municipal decision-support and do NOT generate 15-minute hydrodynamic flood-surge hydrographs.
2. **Live Warnings vs. Daily Forecasts:** Daily forecasts do NOT replace real-time emergency telemetry warnings. Immediate evacuation decisions must be based on live gauge heights served via Path A (`/api/status`).
3. **Tumana Target Semantics:** Tumana model output represents PAGASA daily observations and cannot be mapped to municipal flood severity stages (Alert, Alarm, Critical).
4. **Baseflow Persistence Behavior:** During extended dry spells with negligible rainfall, persistence ($\hat{y}_t = y_{t-1}$) can achieve slightly lower MAE than MLR models. MLR models are optimized to capture hydrologically significant rainfall-driven flood events.
5. **External Telemetry Dependency:** In the event of upstream rainfall sensor outages, the system gracefully falls back to persistence mode. If in-situ gauge telemetry is missing, the system outputs `unavailable` rather than guessing.
