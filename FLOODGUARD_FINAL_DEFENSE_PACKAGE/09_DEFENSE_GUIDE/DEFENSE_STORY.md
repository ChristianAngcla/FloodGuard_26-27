# FloodGuard Defense Narrative & Engineering Story

## 1. The Core Operational Need
The Marikina River Basin requires reliable day-ahead municipal decision support to assist local disaster management authorities in planning resources, staging evacuation shelters, and alerting communities.

## 2. Methodological Foundation
FloodGuard implements Multiple Linear Regression (MLR) models fitted via Ordinary Least Squares (OLS) with:
- Strict 24/24 hourly data quality gates (100% complete hourly records required for daily aggregates).
- Historically predictive lagged water-level and rainfall variables retained under the frozen research methodology.
- HC3 robust standard errors for honest hypothesis testing under heteroskedasticity.
- Variance Inflation Factor (VIF) screening confirming absence of severe multicollinearity.

## 3. Engineering Rigor & Production Governance
The system bridges statistical modeling with full production architecture:
- Strict Two-Path separation between real-time emergency telemetry alarms (Path A) and day-ahead forecast planning (Path B).
- Truthful missing telemetry handling (missing sensors return `null` with explicit unavailability status).
- Atomic, deduplicated FCM notifications sent to verified canonical barangay topics.
- Controlled yearly recalibration with super-admin password reconfirmation and instant rollback.
