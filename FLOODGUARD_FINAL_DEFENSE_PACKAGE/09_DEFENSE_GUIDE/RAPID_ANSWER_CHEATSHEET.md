# RAPID ANSWER DEFENSE CHEATSHEET

### 1. What are the certified models?
- **Sto. Niño:** Candidate 9 (AR2 with lag-1 & lag-3 + Boso-Boso Rain lag-1). Refit N=2,441, R²=0.8988, Max VIF = 2.0610.
- **Nangka:** Candidate 4 (AR1 + Boso-Boso Rain lag-1). Refit N=2,128, R²=0.4335, Max VIF = 1.5957.
- **Tumana:** Candidate 8 (AR1 + Science Garden Rain lag-1). Refit N=1,648, R²=0.8426, Max VIF = 1.1212.

### 2. What are the station thresholds?
- **Sto. Niño:** Alert 15.00 m, Alarm 16.00 m, Critical 17.00 m
- **Nangka:** Alert 16.50 m, Alarm 17.10 m, Critical 17.70 m
- **Tumana:** Alert 17.26 m, Alarm 18.26 m, Critical 19.26 m (PAGASA FFWS official EL.m datum)

### 3. What is the Two-Path Architecture?
- **Path A (Live Monitoring):** Real-time sensor readings compared against official station thresholds for live emergency alerting.
- **Path B (Daily Forecasting):** MLR model runs daily to predict the next-calendar-day water level for decision support.
- Daily forecast predictions **never** trigger live emergency evacuation warnings.
