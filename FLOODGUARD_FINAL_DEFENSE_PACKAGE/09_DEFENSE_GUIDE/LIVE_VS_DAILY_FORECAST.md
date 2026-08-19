# TWO-PATH ARCHITECTURE: LIVE EMERGENCY MONITORING VS DAILY FORECASTING

## 1. Architectural Distinction
- **Path A — Live Emergency Monitoring:**
  - Evaluates actual current sensor reading vs official warning thresholds:
    - Sto. Niño: 15.00 / 16.00 / 17.00 m
    - Nangka: 16.50 / 17.10 / 17.70 m
    - Tumana: 17.26 / 18.26 / 19.26 m
  - Generates immediate live emergency alerts and citizen mobile push notifications upon state transition / escalation.
- **Path B — Next-Calendar-Day Daily Decision-Support Forecasting:**
  - Evaluates certified MLR equations using completed historical lags.
  - Generates next-calendar-day water level prediction with advisory forecast bands.
  - Daily forecasts are planning guidance and **never** trigger live emergency evacuation alerts.
