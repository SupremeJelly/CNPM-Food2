# PORTS — Tóm tắt nhanh

Mục đích: ghi ngắn gọn các cổng dùng cho dev/local trong project, bao gồm cả cổng đã đổi và cổng cần kiểm tra.

---

## Bản tóm tắt (ngắn)

- **Frontend**: `4200` → `4300` — ĐÃ đổi
  - Files: `frontend/package.json`, `k8s/services/frontend-deployment.yaml`, `frontend/src/environments/enviroment.ts`
- **API Gateway**: `9000` → `9001` — ĐÃ đổi
  - Files: `api-gateway/src/main/resources/application.yaml`, `k8s/services/api-gateway-deployment.yaml`
- **User service**: `8081` → `8181` — ĐÃ đổi
  - Files: `user-service/src/main/resources/application.properties`, `k8s/services/user-service-deployment.yaml`
- **Restaurant service**: `8082` → `8182` — ĐÃ đổi
  - Files: `k8s/services/restaurant-service-deployment.yaml`
- **Order service**: `8083` → `8183` — ĐÃ đổi (xác minh: có vài chỗ từng ghi `8084` trước đây)
  - Files: `k8s/services/order-service-deployment.yaml`
- **Payment service**: `8086` → `8184` — ĐÃ đổi
  - Files: `k8s/services/payment-service-deployment.yaml`

---

## MySQL / cơ sở dữ liệu

- **Host MySQL**: `3306` → **Khuyến nghị** `3307` — *kiểm tra/áp dụng* (cần xác nhận tất cả chỗ liên quan trong `docker-compose.yml` và `render-env/*.env`)

---

## Port còn **cần kiểm tra** (khả năng còn sót trong repo)

- `8081`, `8082`, `8083`, `8084`, `8085`, `8086` — các port backend cũ (một số đã được đổi, vẫn nên chạy tìm kiếm toàn repo để xác nhận)
- `4200`, `9000` — frontend / api-gateway cũ (một số đã được đổi)
- `3306` — MySQL host (nếu muốn chuyển sang `3307`, cần kiểm tra tất cả chỗ sử dụng)

---

## Lệnh nhanh kiểm tra cổng đang lắng nghe (Windows PowerShell)

```powershell
Get-NetTCPConnection -State Listen | Where-Object {$_.LocalPort -in 8181,8182,8183,8184,3307} |
  Select-Object LocalAddress,LocalPort,OwningProcess | Sort-Object LocalPort | Format-Table -AutoSize
```

## Lệnh nhanh tìm tham chiếu cổng trong repo

```powershell
git grep -n "8081\|8082\|8083\|8084\|8085\|8086\|4200\|9000\|3306" || echo "No matches"
```

---

Ghi chú ngắn: file này chỉ tóm tắt hiện trạng và điểm cần kiểm tra; nếu muốn tôi có thể: (1) chạy lệnh tìm kiếm toàn repo và cập nhật phần "Port còn cần kiểm tra" với kết quả, hoặc (2) tạo PR với các thay đổi port đã áp dụng.
