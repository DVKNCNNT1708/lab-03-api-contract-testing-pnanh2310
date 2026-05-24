# Reliability Checklist — FIT4110 Lab 03

Điền checklist này trước khi nộp Lab 03.

## 1. Functional tests

- [ ] Có test cho endpoint health.
- [ ] Có test happy path cho endpoint chính.
- [ ] Có kiểm tra status code 2xx.
- [ ] Có kiểm tra field quan trọng trong response.
- [ ] Có ít nhất 1 test đọc dữ liệu danh sách hoặc chi tiết.

## 2. Auth tests

- [ ] Có test thiếu token.
- [ ] Có test sai token hoặc token rỗng.
- [ ] Endpoint public được khai báo rõ nếu không cần auth.
- [ ] Test thể hiện đúng expected status 401/403.

## 3. Negative tests

- [ ] Có test thiếu field bắt buộc.
- [ ] Có test sai kiểu dữ liệu.
- [ ] Có test sai enum hoặc giá trị ngoài miền.
- [ ] Lỗi trả về theo cùng một error model.

## 4. Boundary tests

- [ ] Có test min/max hoặc dữ liệu sát ngưỡng.
- [ ] Có test limit/pagination nếu endpoint có danh sách.
- [ ] Có test payload lớn hoặc metadata thiếu.
- [ ] Có ghi chú kỳ vọng xử lý dữ liệu biên.

## 5. Reliability tests cơ bản

- [ ] Có kiểm tra response time.
- [ ] Có mô tả timeout mong muốn.
- [ ] Có test hoặc ghi chú retry/idempotency nếu phù hợp.
- [ ] Có consumer-side smoke test với ít nhất 1 mock của nhóm khác.

## 6. Evidence

- [ ] Collection export JSON.
- [ ] Environment mock export JSON.
- [ ] Environment local export JSON.
- [ ] Newman report XML/HTML.
- [ ] Test-case matrix đã điền.
- [ ] Biên bản handshake đã điền.
# Reliability Checklist

## Health Check
- [x] `/health` endpoint implemented
- [x] Service availability validation supported

## Error Handling
- [x] 400 validation errors documented
- [x] 401 unauthorized errors documented
- [x] 404 resource not found documented
- [x] 500 internal server error documented

## Retry Strategy
- [x] Clients may retry GET requests safely
- [x] PATCH requests designed to avoid duplicate side effects

## Timeout Handling
- [x] API gateway timeout expected under 30 seconds
- [x] Consumer timeout strategy documented

## Observability
- [x] Request IDs supported
- [x] Health endpoint available
- [x] Error responses standardized

## Security
- [x] Bearer authentication configured
- [x] Sensitive endpoints protected

## Pagination
- [x] Cursor pagination supported
- [x] Limit parameter validated

## Contract Validation
- [x] OpenAPI contract validated with Spectral
- [x] Mock server validated using Prism
- [x] Postman contract tests executed
