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
- **Sprint 3 (Hoàn thành)**: Giám sát deployment tự động từ GitHub sang Vercel, kiểm thử luồng CI/CD Auto-Deploy.
- **Sprint 4 (Hoàn thành)**: Khắc phục lỗi tự động nộp Google Indexing API & tự động cập nhật mốc thời gian indexed_at; Bổ sung cột Telegram SEO Status, nút ✈️ Share Telegram Hàng Loạt và sửa lỗi đóng khối ngoặc render bảng Telegram Tab.
- **Sprint 5**: Chuẩn hóa Webhook Make.com kết nối Facebook Pages: Tự động trích xuất đến 4 hình ảnh (`image1..4` và mảng `facebook_photos` dạng `[{ url }]`), sinh Hashtag CamelCase thông minh (`generateSmartHashtags`) và format nội dung bài viết bắt mắt (`formatted_content`). Pushed & Deployed Vercel thành công cho cả `thohong` và `DHTK`.
- **Sprint 6**: Khắc phục lỗi Facebook Pages `CreatePostWithPhotos` trên Make.com: Đã bổ sung thuộc tính `type: 'url'` cho mảng `facebook_photos` khớp schema Make.com, đồng thời nâng cấp toàn bộ luồng Blog AI Generator (`/api/admin/blog/generate`): Tự động lọc chính xác 5 sản phẩm khớp từ khóa SEO bài viết trong CSDL kho hàng, tự động bổ sung nguồn ảnh HD Internet (Unsplash) chuẩn ngành hàng khi CSDL thiếu ảnh, giữ nguyên luồng Tự động Xuất bản (Auto-Publish) đa kênh.
- **Sprint 7 (Hoàn thành)**: Audit toàn diện & nâng cấp Menu Admin CP Make.com Automation: Khắc phục lỗ hổng bảo mật rò rỉ Webhook URL trên public API `/api/settings`, sửa lỗi không auto-fill dữ liệu Webhook khi mở Admin Panel, tôn trọng cờ bật/tắt Auto Share `autoMakeShare`, chuẩn hóa giao diện Collapsible Sections (`UI_MAP.md`) và bổ sung trạng thái Loading nút Share đơn lẻ.
