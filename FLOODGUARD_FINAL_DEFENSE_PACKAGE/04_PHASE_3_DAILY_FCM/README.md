# Phase 3 — Daily FCM Advisory Notification Dispatcher

## Summary
Phase 3 establishes the atomic, deduplicated daily FCM notification dispatcher (`server/services/dailyFcmDispatcher.js`), canonical barangay topics (`barangay_<name>`), and strict prohibition of threshold wording in Tumana advisories.

## Primary Evidence Files
1. `FLOODGUARD_PHASE_3_FINAL_FCM_REPORT.md`: Report on notification governance, atomic concurrency locks, and topic formatting.
2. `PHASE_3_FINAL_FCM_TEST_OUTPUT.txt`: Automated test output verifying deduplication and dispatch rules.
3. `FLOODGUARD_PHASE_3_FINAL_FCM_REVIEW_BUNDLE.zip`: Complete sealed review bundle for Phase 3.
4. `FLOODGUARD_PHASE_3_FINAL_FCM_REVIEW_BUNDLE_CHECKSUM.txt`: SHA-256 verification hash.
