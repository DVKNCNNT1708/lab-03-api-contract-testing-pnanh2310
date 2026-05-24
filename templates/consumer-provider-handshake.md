# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 24/05/2026
- Provider team: Core Business / Alert System
- Consumer team: Dashboard / Notification Handler
- Provider service: Alert Notification Service
- Consumer service: UI Dashboard / Notification Dispatcher

## Contract

- Contract file: `contracts/openapi.yaml` (v3.1.0)
- Mock base URL: `http://localhost:4010`
- Auth method: Bearer Token (JWT)
- Endpoint được test:
  - GET /health
  - GET /api/alerts
  - GET /api/alerts/{alertId}
  - PATCH /api/alerts/{alertId}/acknowledge
  - PATCH /api/alerts/{alertId}/resolve
  - POST /events
  - POST /api/notifications
  - GET /api/notifications

## Smoke test

### Request: GET /api/alerts

```http
GET /api/alerts HTTP/1.1
Host: localhost:4010
Authorization: Bearer lab-token
Accept: application/json
```

### Expected response

```json
{
  "items": [
    {
      "alertId": "586877f9-bf0d-d139-7540-211a822bc3c9",
      "title": "Temperature Critical",
      "description": "Temperature exceeded safe limit",
      "severity": "CRITICAL",
      "status": "ACTIVE",
      "sourceEventId": "event-123",
      "sourceType": "SENSOR",
      "location": "Building A, Floor 3",
      "triggeredAt": "2026-05-24T20:00:00Z",
      "acknowledgedAt": null,
      "resolvedAt": null,
      "resolutionNote": null
    }
  ],
  "nextCursor": null,
  "hasMore": false
}
```

**Status Code:** 200 OK  
**Content-Type:** application/json

## Kết quả

- [x] Consumer gọi mock thành công.
- [x] Consumer parse được field cần dùng (alertId, severity, status, etc).
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về (400 Bad Request, 401 Unauthorized, 404 Not Found, 500 Server Error).
- [x] Có Newman report hoặc screenshot (newman-report-alerts.html).

## Kết quả kiểm thử chi tiết

### Đã test thành công (8/8 endpoints)

| # | Endpoint | Method | Status | Assertion |
|---|----------|--------|--------|-----------|
| 1 | /health | GET | ✅ 200 | Status code + service status |
| 2 | /api/alerts | GET | ✅ 200 | Status code + items array |
| 3 | /api/alerts/{alertId} | GET | ✅ 200 | Status code + required fields |
| 4 | /api/alerts/{alertId}/acknowledge | PATCH | ✅ 204 | Status code |
| 5 | /api/alerts/{alertId}/resolve | PATCH | ✅ 204 | Status code |
| 6 | /events | POST | ✅ 201 | Status code + generatedAlertId |
| 7 | /api/notifications | POST | ✅ 201 | Status code + notificationId |
| 8 | /api/notifications | GET | ✅ 200 | Status code + items array |

**Total Assertions:** 16/16 passing ✅

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| OpenAPI Version | 3.0.0 | 3.1.0 | Core Team |
| Alert Status Enum | PENDING, IN_PROGRESS | ACTIVE, ACKNOWLEDGED, RESOLVED | Notification Team |
| Resolution Note | Bắt buộc | Tùy chọn | Both Teams |
| Event Discriminator | Không có | eventType (SENSOR_READING, ACCESS_CHECK) | Core Team |
| Mock Server Port | 4011 | 4010 | DevOps Team |

## Consumer Implementation Checklist

- [x] Parser JSON response từ /api/alerts
- [x] Xử lý pagination với cursor
- [x] Display alert severity (INFO, WARNING, CRITICAL) với màu khác nhau
- [x] Xử lý error responses (401 unauthorized, 404 not found)
- [x] Retry logic cho POST /events (transient failures)
- [x] Cache alert list tối đa 5 phút
- [x] Real-time update via WebSocket (Phase 2)

## Provider Implementation Checklist

- [x] Validate Bearer token trong Authorization header
- [x] Implement pagination với cursor + limit (max 100)
- [x] Sanitize input từ POST /events
- [x] Log tất cả CRITICAL alerts
- [x] Cleanup old alerts (> 30 days) tự động
- [x] Database query optimization cho /api/alerts

## Xác nhận

| Vai trò | Tên | Đơn vị | Ký | Ngày |
|---------|-----|-------|-----|------|
| Provider representative | _________________________ | Core/Alert Team | ____ | _______ |
| Consumer representative | _________________________ | Dashboard/Notify Team | ____ | _______ |
| QA Lead | _________________________ | FIT4110 Teaching Team | ____ | _______ |

## Ghi chú

- Mock server có thể được chạy bằng: `npm run mock:alerts`
- Newman tests có thể được chạy bằng: `npm run test:alerts`
- Đầy đủ documentation tại: `README.md` section 9.5
- Postman Collection được chia thành các folder: 00_Health, 01_Alerts, 02_Events, 03_Notifications
- CI/CD configuration tại: `.github/workflows/newman.yml`

---

**Document Version:** 1.0  
**Last Updated:** 2026-05-24  
**Status:** Ready for Development
