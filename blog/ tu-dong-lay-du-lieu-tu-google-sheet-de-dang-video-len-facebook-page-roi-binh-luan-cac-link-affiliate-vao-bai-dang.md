```markdown
---
slug: tu-dong-lay-du-lieu-tu-google-sheet-de-dang-video-len-facebook-page-roi-binh-luan-cac-link-affiliate-vao-bai-dang
title: 'Template: Tự động lấy dữ liệu từ Google Sheet để đăng video lên Facebook Page rồi bình luận các link affiliate vào bài đăng.'
authors: [gemini-bot]
tags: [n8n, template, automation, ai]
---

## 🎯 Kết quả đạt được khi sử dụng mẫu này

Mẫu workflow này giúp bạn tự động hóa hoàn toàn quy trình marketing trên Facebook Page. Chỉ cần chuẩn bị nội dung trong Google Sheet, n8n sẽ lo phần còn lại.

-   🚀 **Tự động đăng video:** Lấy link video và nội dung bài đăng từ các hàng trong Google Sheet để đăng lên Facebook Page.
-   🔗 **Tự động bình luận:** Ngay sau khi đăng video thành công, workflow sẽ tự động bình luận các link affiliate (hoặc bất kỳ link nào bạn muốn) vào chính bài đăng đó.
-   📊 **Quản lý nội dung hiệu quả:** Tự động cập nhật trạng thái "Đã đăng" trong Google Sheet để tránh đăng lại nội dung cũ.
-   ⏰ **Tiết kiệm thời gian:** Giải phóng bạn khỏi các thao tác đăng bài và bình luận thủ công lặp đi lặp lại.
-   📈 **Tăng hiệu suất:** Dễ dàng lên lịch và đăng hàng loạt video, tối ưu hóa chiến dịch affiliate marketing của bạn.

---

## ⚙️ Yêu cầu cần thiết

Để sử dụng mẫu này, bạn cần chuẩn bị các tài khoản và thông tin sau:

-   **Tài khoản n8n:** Có thể là n8n cloud hoặc self-hosted.
-   **Tài khoản Google:** Đã kết nối với n8n thông qua **Credentials** (OAuth2).
-   **Tài khoản Facebook Developer:** Cần có một App với các quyền `pages_manage_posts` và `pages_read_engagement`.
-   **Facebook Page Credentials:** Đã kết nối tài khoản Facebook của bạn (có quyền quản trị Page) với n8n thông qua **Credentials** (OAuth2).
-   **Một file Google Sheet** được cấu hình với các cột tối thiểu như:
    -   `video_url`: Chứa link URL công khai của video cần đăng.
    -   `post_content`: Nội dung văn bản cho bài đăng.
    -   `affiliate_links`: Các link affiliate bạn muốn bình luận, có thể phân cách bằng dấu phẩy (ví dụ: `link1.com, link2.com`).
    -   `status`: Cột để theo dõi trạng thái, ví dụ: để trống hoặc "pending" cho các bài chưa đăng.

**Biến môi trường cần điền**:
-   Không bắt buộc, nhưng bạn có thể tạo biến môi trường cho `FACEBOOK_PAGE_ID` để dễ dàng thay đổi Page nếu cần.

---

## 📥 Cách import & lưu ý

### ✅ Import vào n8n
1. Mở n8n → click **Import Workflow**
2. Chọn **Tải file JSON** hoặc **Paste JSON bên dưới**
3. Bấm **Save & Activate**

### 💡 Lưu ý
-   **Cấu hình Node `Google Sheets`:**
    -   Trong node `Get New Rows`, hãy chọn đúng **Credential**, **Sheet ID**, **Sheet Name** và **Range** (ví dụ: `A:D`).
    -   Workflow được thiết kế để chỉ lấy các hàng có cột `status` trống.
-   **Cấu hình Node `Facebook Pages (Post Video)`:**
    -   Chọn **Credential** Facebook của bạn.
    -   Điền **Page ID** của trang bạn muốn đăng.
-   **Cấu hình Node `Facebook Pages (Create Comment)`:**
    -   Node này đã được thiết lập để tự động lấy `Post ID` từ node đăng video trước đó.
    -   Nó sẽ gộp tất cả các link trong cột `affiliate_links` vào một bình luận duy nhất. Nếu bạn muốn mỗi link là một bình luận riêng, bạn cần thêm node `SplitInBatches` trước node này.
-   **Cấu hình Node `Google Sheets (Update Row)`:**
    -   Đảm bảo node này chọn đúng **Sheet ID** và **Sheet Name**. Nó sẽ tự động cập nhật cột `status` thành "Đã đăng" để không bị lấy lại ở lần chạy sau.
-   **Trigger (Kích hoạt):**
    -   Mặc định, workflow này cần được kích hoạt thủ công (**Manual Trigger**).
    -   Để tự động hóa hoàn toàn, hãy thay thế node `Manual Trigger` bằng node `Cron` và đặt lịch chạy bạn muốn (ví dụ: mỗi ngày một lần).
```