# MY FINANCE v1 — Hướng dẫn cài đặt

Ứng dụng web quản lý thu chi cá nhân: đăng nhập, thêm/sửa/xóa giao dịch, đính kèm ảnh tùy chọn, lịch sử tìm kiếm/lọc, báo cáo theo kỳ, biểu đồ tròn, nhận định tự động và xuất Excel.

## Các file
- `index.html`: giao diện.
- `styles.css`: thiết kế responsive.
- `app.js`: xử lý ứng dụng.
- `firebase-config.js`: cấu hình Firebase cần điền.
- `firestore.rules`: quy tắc Firestore.
- `storage.rules`: quy tắc Firebase Storage.

## 1. Cấu hình Firebase
1. Mở https://console.firebase.google.com/ và tạo project.
2. Project settings → General → Your apps → Add app → Web. Sao chép cấu hình vào `firebase-config.js`.
3. Authentication → Sign-in method: bật Email/Password.
4. Tạo Firestore Database, mở Rules, dán nội dung `firestore.rules` rồi Publish.
5. Trong Authentication → Settings → Authorized domains, thêm domain GitHub Pages sau khi triển khai.

## 2. Hình ảnh (tùy chọn)
Ứng dụng dùng Firebase Storage để đồng bộ ảnh. Tạo/bật Storage và dán `storage.rules` vào phần Rules. Kiểm tra Billing/Usage và yêu cầu gói hiện hành trước khi bật Storage; không nâng cấp gói nếu bạn chưa chấp thuận chi phí. Nếu chưa cấu hình Storage, vẫn có thể ghi giao dịch miễn là không đính kèm ảnh.

## 3. Đăng lên GitHub Pages
1. Tạo repository mới, ví dụ `my-finance`.
2. Tải lên `index.html`, `styles.css`, `app.js`, `firebase-config.js`.
3. Settings → Pages → chọn branch `main`, thư mục `/(root)` → Save.
4. Chờ GitHub Pages tạo địa chỉ, rồi thêm domain đó vào Firebase Authentication → Authorized domains.
5. Mở website, chọn “Tạo tài khoản” để đăng ký.

Hai tệp `firestore.rules` và `storage.rules` phải được dán vào Firebase Console; GitHub Pages không tự triển khai quy tắc.

## 4. Bảo mật và ghi chú
- Mỗi giao dịch gắn `ownerId`; Firestore Rules giới hạn người dùng vào dữ liệu của chính họ.
- Không mở quyền đọc/ghi công khai trong Security Rules.
- Firebase Web config có thể xuất hiện trong mã trình duyệt; điều quan trọng là Authentication và Rules phải được cấu hình đúng.
- “Chênh lệch thu chi” = tổng thu trừ tổng chi trong kỳ, không phải số dư thực tế trong ví/ngân hàng.
- Nhận định là phép thống kê theo quy tắc, không phải tư vấn tài chính.
- Xuất Excel chỉ xuất các giao dịch đang hiện theo bộ lọc lịch sử. Ảnh được xuất dưới dạng đường dẫn.
- Ngày giao dịch được lưu theo định dạng `YYYY-MM-DD`.
