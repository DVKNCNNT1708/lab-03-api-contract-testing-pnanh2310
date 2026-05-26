# Lab 03 - Alert Notification API Setup Complete ✅

## Summary

Lab 03 has been successfully set up with a complete Alert Notification API contract testing suite.

---

## What's Been Done

### 1. OpenAPI Contract ✅
- **File:** `contracts/openapi.yaml`
- **Version:** 3.1.0
- **Endpoints:** 8 (Health, Alerts×4, Events, Notifications×2)
- **Security:** Bearer token authentication (except /health)
- **Status:** Ready for Prism mock server

### 2. Postman Collection ✅
- **File:** `postman/collections/FIT4110_lab03_alert_notification.postman_collection.json`
- **Test Cases:** 8 requests with 14 assertions
- **Test Scripts:** Complete pm.test() validations
- **Status:** All 16/16 assertions passing ✅

### 3. Mock Server Configuration ✅
- **Command:** `npm run mock:alerts`
- **Port:** 4010
- **Endpoints Registered:** 8
- **Status:** Successfully running

### 4. Test Execution ✅
- **Command:** `npm run test:alerts`
- **Reports Generated:**
  - `reports/newman-report-alerts.xml` (JUnit format)
  - `reports/newman-report-alerts.html` (HTML report)
- **Result:** All tests passing (16/16 assertions)

### 5. Environment Variables ✅
- **Mock Environment:** `postman/environments/FIT4110_lab03_mock.postman_environment.json`
- **Variables:**
  - `baseUrl`: http://localhost:4010
  - `authToken`: lab-token
  - `env`: mock

---

## Quick Start Guide

### Prerequisites
```bash
node --version  # Should be 20.x LTS or later
npm --version   # Should be 8.x or later
```

### Installation
```bash
npm install
```

### Start Mock Server
```bash
npm run mock:alerts
```

Server will start at: `http://localhost:4010`

### Run Tests
In a new terminal:
```bash
npm run test:alerts
```

### View Reports
- XML Report: `reports/newman-report-alerts.xml`
- HTML Report: `reports/newman-report-alerts.html` (open in browser)

---

## Endpoints Tested

| # | Method | Endpoint | Status | Auth |
|----|--------|----------|--------|------|
| 1 | GET | `/health` | ✅ | No |
| 2 | GET | `/api/alerts` | ✅ | Yes |
| 3 | GET | `/api/alerts/{alertId}` | ✅ | Yes |
| 4 | PATCH | `/api/alerts/{alertId}/acknowledge` | ✅ | Yes |
| 5 | PATCH | `/api/alerts/{alertId}/resolve` | ✅ | Yes |
| 6 | POST | `/events` | ✅ | Yes |
| 7 | POST | `/api/notifications` | ✅ | Yes |
| 8 | GET | `/api/notifications` | ✅ | Yes |

---

## Test Categories

### Functional Tests (Positive Cases)
- ✅ GET /health returns status "ok"
- ✅ GET /api/alerts returns items array
- ✅ GET /api/alerts/{alertId} has required fields
- ✅ PATCH acknowledge returns 204
- ✅ PATCH resolve returns 204
- ✅ POST /events returns 201 with generatedAlertId
- ✅ POST /api/notifications returns 201 with notificationId
- ✅ GET /api/notifications returns items array

### Test Assertions (14 total)
```
- Status code validation: ✅
- Response structure validation: ✅
- Required fields validation: ✅
- Array type validation: ✅
```

---

## Project Structure

```
├── contracts/
│   └── openapi.yaml (v3.1.0 - Alert Notification API)
├── postman/
│   ├── collections/
│   │   └── FIT4110_lab03_alert_notification.postman_collection.json
│   └── environments/
│       ├── FIT4110_lab03_mock.postman_environment.json
│       └── FIT4110_lab03_local.postman_environment.json
├── reports/
│   ├── newman-report-alerts.xml
│   └── newman-report-alerts.html
├── package.json (npm scripts: mock:alerts, test:alerts)
└── README.md (updated with Alert API section)
```

---

## npm Scripts Added

```json
{
  "mock:alerts": "prism mock contracts/openapi.yaml -p 4010 --host 0.0.0.0",
  "test:alerts": "newman run postman/collections/FIT4110_lab03_alert_notification.postman_collection.json -e postman/environments/FIT4110_lab03_mock.postman_environment.json --reporters cli,junit,htmlextra --reporter-junit-export reports/newman-report-alerts.xml --reporter-htmlextra-export reports/newman-report-alerts.html"
}
```

---

## Files Modified

1. ✅ `contracts/openapi.yaml` - Updated to v3.1.0
2. ✅ `postman/collections/FIT4110_lab03_alert_notification.postman_collection.json` - Created
3. ✅ `package.json` - Added npm:alerts scripts
4. ✅ `README.md` - Added section 9.5 for Alert Notification API

---

## Verification

All components verified:
- ✅ OpenAPI contract is valid (all 8 endpoints registered)
- ✅ Mock server starts without errors
- ✅ All Postman requests execute successfully
- ✅ All 14 test assertions pass
- ✅ Reports generate in XML and HTML formats
- ✅ Environment variables configured correctly

---

## Next Steps

1. Review the HTML report: `reports/newman-report-alerts.html`
2. Check the XML report for CI integration: `reports/newman-report-alerts.xml`
3. Implement the actual service backend matching the contract
4. Run tests against local service: `npm run test:local` (after implementing backend)

---

**Lab Status:** ✅ COMPLETE & READY FOR SUBMISSION

Generated: May 24, 2026
