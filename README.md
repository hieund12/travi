# travi

# 🛡️ Bảo Vệ Dự Án GitHub cá nhân Với Trivy + ClamAV + YARA + License Scan

## 📌 Giới thiệu

Khi bạn phát triển hoặc **fork một dự án mã nguồn mở** trên GitHub, có nhiều rủi ro liên quan đến:
- **Thư viện có bản quyền không tương thích**
- **Code chứa mã độc/phishing/virus**
- **Thêm code lạ từ người khác qua pull request/commit**

Bộ cấu hình GitHub Actions bên dưới sẽ giúp bạn **tự động phát hiện** các rủi ro này.

---

## 🧾 Danh sách workflow GitHub Actions

| File | Mục đích | Kích hoạt khi nào |
|------|----------|-------------------|
| `license-check.yml` | Kiểm tra bản quyền các thư viện dùng trong dự án | Mỗi lần push hoặc pull request |
| `security-full-scan.yml` | Quét toàn bộ mã độc (Trivy + ClamAV + YARA) | Khi fork một dự án mới hoặc thủ công qua nút “Run workflow” |
| `trivy.yml` | Tự động quét khi có commit mới để kiểm tra secrets, malware | Khi có ai đó commit vào repo của bạn |

---

## 🧪 Chi tiết từng workflow

### 1️⃣ `license-check.yml` – Kiểm tra bản quyền thư viện

Giúp bạn phát hiện nếu dự án có sử dụng thư viện:
- **Không được phép thương mại hóa**
- **Không tương thích với MIT/BSD/GPL** của bạn

✅ Tự động báo lỗi nếu có thư viện **vi phạm license policy**.

> 📂 File cần: `license-policy.yaml` để định nghĩa các license được phép.

---

### 2️⃣ `security-full-scan.yml` – Quét toàn diện mã độc

Kết hợp:
- 🔍 **Trivy** để tìm **secrets** và file nguy hiểm
- 🦠 **ClamAV** để phát hiện **virus, phishing mẫu**
- 🧬 **YARA** để quét mẫu **malware, exploit pattern** nâng cao

👉 Rất hữu ích khi bạn **fork một dự án online lạ** hoặc muốn kiểm tra **toàn bộ source trước khi phát hành**.

> 📦 Các kết quả được ghi vào log và tải lên dạng artifact (`trivy_output.log`, `clamav_output.log`, `yara_output.log`, `summary.log`)

---

### 3️⃣ `trivy.yml` – Kiểm tra mỗi commit vào repo

Dành cho repo công khai khi:
- Nhận pull request từ người khác
- Muốn đảm bảo **mỗi thay đổi không chứa secrets/API keys**

🛡️ Dùng **Trivy** để kiểm tra:
- Secrets trong code
- Mã độc đơn giản

---

## 🚀 Cách sử dụng

1. Copy các file `.yml` vào thư mục `.github/workflows/` của repo bạn.
2. (Tuỳ chọn) Thêm file `license-policy.yaml` nếu muốn kiểm soát license rõ ràng.
3. Dùng tab **Actions** trên GitHub để theo dõi kết quả mỗi lần chạy.

---

## 📷 Minh họa kết quả
- ✅ ClamAV báo không có virus
- ✅ Trivy không phát hiện secrets
- ⚠️ YARA match nhiều mẫu PDF/XSS/phishing ⇒ cần kiểm tra thêm

---

## 🤝 Đóng góp

Bạn có thể fork và nâng cấp các rule, hoặc tạo thêm quy tắc riêng cho `trivy`, `clamav`, `yara`.

---

## 📫 Liên hệ

Được thiết kế và duy trì bởi @tcode0x
