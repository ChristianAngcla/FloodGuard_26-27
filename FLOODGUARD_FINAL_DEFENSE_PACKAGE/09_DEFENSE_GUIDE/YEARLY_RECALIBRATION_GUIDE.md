# Controlled Yearly Recalibration & Statistical Governance (Phase 5)

## 1. Governance Workflow Overview
1. **Upload & Schema Validation (`/api/calibration/upload`):** Super-admin uploads new verified yearly daily CSV. The server validates headers, column aliases, date ranges, and checks for overlap with protected history.
2. **Two-Stage Historical Merge & Complete-Case OLS (`/api/calibration/run`):** The server merges protected historical baseline with uploaded yearly rows, builds exact calendar lags, and executes pure OLS $(X^T X)^{-1} X^T y$.
3. **Automated Diagnostic Gates:** Computes $R^2$, MAE, RMSE, HC3 robust standard errors, $t$-statistics, $p$-values, and VIF for every predictor. If VIF $> 5.0$ or matrix is singular, approval is blocked.
4. **Super-Admin Approval (`/api/calibration/approve`):** Super-admin reviews diagnostics and approves the calibration candidate.
5. **Password-Reconfirmed Activation (`/api/calibration/activate`):** Super-admin re-enters account password (verified via bcrypt). Server deploys the new model version into `ActiveModelVersion` collection.
6. **One-Click Instant Rollback (`/api/calibration/rollback`):** Super-admin can instantly revert active models to canonical baseline with password reconfirmation.

## 2. Security Guarantees
- **No Client-Side Coefficients:** Clients cannot submit custom $\beta$ parameters. The server fits all models internally.
- **Decommissioned Endpoints:** Legacy `/api/train` and `/api/train/save` endpoints permanently return `HTTP 410 Gone`.
- **Immutable Audit Trail:** All uploads, runs, approvals, activations, and rollbacks are logged to `CalibrationAuditLog`.
