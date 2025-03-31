# My-Nuclei-Template
# Fuzzing API for Buffer Overflow and Invalid Input

## 🛡 Mục tiêu

Tệp Nuclei template này được thiết kế để phát hiện các lỗ hổng bảo mật trong API, tập trung vào:

- **Buffer Overflow** (Tràn bộ đệm)
- **Xác thực đầu vào không hợp lệ**
- **Injection Attacks** như SQL Injection, XSS

## 📄 Thông tin Template

- **ID**: `fuzzing-buffer-overflow-invalid-input`
- **Tác giả**: TranDieuQuynh
- **Mức độ nghiêm trọng**: High
- **Endpoint kiểm tra**: `/api/login`
- **Phương thức HTTP**: `POST`
- **Content-Type**: `application/json`

## 🔍 Payloads và kỹ thuật fuzzing

Template sử dụng các kỹ thuật fuzzing để gửi dữ liệu lớn, đặc biệt hoặc nguy hiểm tới API, ví dụ:

- Chuỗi ngẫu nhiên dài: `{{RandomString(1000)}}`, `{{RandomString(10000)}}`
- Ký tự đặc biệt: `<script>alert('XSS')</script>`, `' OR '1'='1'`
- Tấn công SQL injection: `'UNION SELECT NULL, username, password FROM users--`

## ✅ Các điều kiện match

### 📌 Nội dung phản hồi (`word matchers`):
Phát hiện các thông báo lỗi phổ biến:

- `"Segmentation fault"`, `"Stack smashing detected"`, `"SQL syntax"`, `"command injection"`...
- Các lỗi về bộ nhớ: `"Out of memory"`, `"Heap corruption"`, `"Invalid memory reference"`

### 📌 Mã trạng thái HTTP (`status matchers`):
- 400, 401, 403, 405, 422, 500

## 🚀 Cách sử dụng

1. Đảm bảo đã cài đặt [Nuclei](https://github.com/projectdiscovery/nuclei)
2. Chạy template với URL cần kiểm tra:

```bash
nuclei -t fuzzing-buffer-overflow-invalid-input.yaml -u https://example.com

Có thể thêm cờ -debug để theo dõi chi tiết:
nuclei -t fuzzing-buffer-overflow-invalid-input.yaml -u https://example.com -debug
