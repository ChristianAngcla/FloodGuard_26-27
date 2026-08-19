# Persistence Fallback & Benchmark Guide

## 1. What is the Persistence Benchmark?
The persistence benchmark is a standard hydrological baseline where tomorrow's water level is projected to be identical to yesterday's observed level:
$$\hat{y}(t) = y(t-1)$$
It is a strong benchmark in hydrological modeling because daily river water levels frequently exhibit high autocorrelation.

## 2. Statistical Comparison Against Certified Models
Performance varies by station and evaluation subset:
- **Sto. Niño:** Persistence achieved the best stated overall retrospective MAE on the 557 exact-common retrospective days, while Candidate 9 had stronger results on the specific examined critical/event subsets versus Candidate 15 and persistence.
- **Nangka:** On Candidate 4's 318 validation dates, persistence had lower MAE (`0.126774 m` vs `0.143768 m`), while Candidate 4 achieved lower RMSE (`0.384644 m` vs `0.440142 m`). Event performance was mixed.
- **Tumana:** Persistence achieved lower validation MAE (`~0.1416 m` vs `~0.1481 m`), while Candidate 8 achieved lower RMSE (`~0.3244 m` vs `~0.3604 m`). Candidate 14 achieved lower RMSE than Candidate 8 (`~0.3101 m`).

## 3. Operational Fallback Logic
If upstream rainfall telemetry is temporarily offline at 07:00 PHT:
- When required in-situ water level lags ($t-1$) are valid but upstream rainfall is missing:
  - The system transitions to `persistence_fallback` mode.
  - Output: $\hat{y}(t) = \text{WL}(t-1)$.
  - `fallbackReason`: Stated upstream rainfall telemetry unavailability.
- When required in-situ water level lags are missing ($t-1$ or $t-3$):
  - The system transitions to `unavailable` mode (`predictedWaterLevel: null`).
  - Prohibitions Enforced: Never substitutes `0.0`, never substitutes `SAFE`, never fabricates numbers.
