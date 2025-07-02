---
slug: workflow-nay-tu-dong-lay-du-lieu-tu-google-sheet-de-dang-video-len-fanpage-facebook-sau-do-binh-luan-cac-link-affiliate-vao-video-vua-dang
title: 'Template: Workflow này tự động lấy dữ liệu từ Google Sheet để đăng video lên Fanpage Facebook, sau đó bình luận các link affiliate vào video vừa đăng.'
authors: [gemini-bot]
tags: [n8n, template, automation, ai]
---

## 🎯 Kết quả đạt được khi sử dụng mẫu này

Mẫu workflow này giúp bạn tự động hóa hoàn toàn quy trình đăng tải video và quảng bá link affiliate trên Fanpage Facebook, biến Google Sheet thành một công cụ lập lịch nội dung mạnh mẽ.
- **Tiết kiệm thời gian:** Lên lịch hàng loạt video chỉ bằng cách điền thông tin vào Google Sheet, không cần thao tác đăng bài thủ công.
- **Tối ưu hóa Affiliate Marketing:** Tự động bình luận các link affiliate ngay sau khi video được đăng, giúp tăng tỷ lệ click mà không làm rối phần mô tả chính của video.
- **Đảm bảo tính nhất quán:** Duy trì luồng nội dung đều đặn trên Fanpage, giúp tăng tương tác và giữ chân người theo dõi.
- **Dễ dàng quản lý:** Toàn bộ kế hoạch nội dung được quản lý tập trung tại một file Google Sheet duy nhất, dễ dàng theo dõi và chỉnh sửa.

---

## ⚙️ Yêu cầu cần thiết

Để workflow hoạt động, bạn cần chuẩn bị các tài khoản và thông tin sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google** đã được cấp quyền truy cập Google Sheets API.
- **Tài khoản Facebook** có quyền Quản trị viên (Admin) của Fanpage bạn muốn đăng bài.
- **Facebook App:** Một ứng dụng được tạo trên nền tảng Facebook for Developers với các quyền sau: `pages_show_list`, `pages_read_engagement`, `pages_manage_posts`.

**Biến môi trường cần điền**:
- `GOOGLE_SHEET_ID`: ID của trang tính Google Sheet chứa dữ liệu (lấy từ URL của trang tính).
- `FACEBOOK_PAGE_ID`: ID của Fanpage Facebook bạn muốn đăng bài.

---

## 📥 Cách import & lưu ý

### ✅ Import vào n8n
1. Mở n8n → click **Import Workflow**
2. Chọn **Tải file JSON** hoặc **Paste JSON bên dưới**
3. Bấm **Save & Activate**

### 💡 Lưu ý
- **Cấu hình Credentials:** Bạn cần kết nối tài khoản Google và Facebook của mình trong các node `Google Sheets` và `Facebook Page`. Click vào node, chọn "Create New" trong mục Credential và làm theo hướng dẫn.
- **Cấu trúc Google Sheet:** Workflow này yêu cầu một cấu trúc Google Sheet cụ thể. Hãy đảm bảo file của bạn có các cột với tiêu đề (hàng đầu tiên) như sau:
    - `video_url`: Chứa đường link URL công khai của file video (ví dụ: link Google Drive đã được chia sẻ công khai).
    - `description`: Nội dung mô tả cho bài đăng video trên Facebook.
    - `affiliate_links`: Các link affiliate cần bình luận, mỗi link cách nhau bởi dấu xuống dòng (Enter).
    - `status`: Cột để workflow cập nhật trạng thái (ví dụ: "Đã đăng"). Bạn cần tạo cột này nhưng có thể để trống.
- **Chọn Fanpage:** Sau khi kết nối tài khoản Facebook, hãy chắc chắn rằng bạn đã chọn đúng Fanpage cần đăng bài trong cài đặt của node `Facebook Page Post`.
- **Node Trigger:** Mẫu này mặc định sử dụng `Cron` node để chạy theo lịch. Bạn có thể thay đổi tần suất hoặc chuyển sang chế độ kích hoạt thủ công (`Manual`) để kiểm tra.
- **Giới hạn API:** Facebook có các giới hạn về tần suất đăng bài. Tránh đặt lịch chạy workflow quá dày đặc để không bị khóa tài khoản.