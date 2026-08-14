# START.md — Nguồn Sự Thật Dự Án Đồng Hành Tiết Kiệm (DHTK)

## 📌 Trạng Thái Hiện Tại
- **Tên dự án**: DHTK Store (Đồng Hành Tiết Kiệm)
- **Repo GitHub**: `https://github.com/nvhung1088-alt/DHTK.git`
- **Vercel Deploy**: `https://dhtk.vercel.app` (Account: `dhtk2026`)
- **Local Server**: `http://localhost:3500` (Cấu hình qua `.env` với `PORT=3500`)
- **Kiến trúc**: Node.js Express + Turso Cloud (SQLite Engine v2 HTTP Pipeline) + Single Page HTML Frontend.
- **Trạng thái**: Hoàn thành migrate sang Turso Cloud, cấu hình bảo mật API `/api/settings/private`, đồng bộ Pancake POS V2 API chuẩn hóa.

## 🎯 Quyết Định Kiến Trúc & Công Nghệ
1. **Turso Engine**: Dùng Native HTTP Client `fetch` gửi payload `/v2/pipeline` trực tiếp tới Turso Cloud, loại bỏ sự phụ thuộc vào SQLite Cục bộ & Tránh lỗi Timeout trên Vercel Serverless.
2. **Pancake POS V2 Push**: Payload truyền `bill_full_name`, `bill_phone_number`, `shipping_address`, `order_sources` chuẩn format V2.
3. **Bảo mật**: Khóa các API route nhạy cảm (`/api/settings/private`, `/api/pos/sync`) bằng JWT authentication.

## 📝 Nhật Ký Sprint
- **Sprint 1 (Hoàn thành)**: Vá lỗ hổng bảo mật API, tách settings private, tích hợp Turso CSDL Cloud.
- **Sprint 2 (Hoàn thành)**: Đồng bộ mã đơn POS Pancake V2 trả về giao diện người dùng, bổ sung Rate Limiter.
- **Sprint 3 (Hiện tại)**: Giám sát deployment tự động từ GitHub sang Vercel, kiểm thử luồng CI/CD Auto-Deploy.
