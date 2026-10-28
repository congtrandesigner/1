# Phòng chat HTML + Firebase

Giao diện là HTML tĩnh, không cần Node.js hay bước build. Firebase cung cấp đăng nhập ẩn danh và đồng bộ tin nhắn giữa những người mở cùng đường link; người dùng không cần tài khoản, tên hay ảnh.

## Cấu hình Firebase một lần

1. Tạo dự án tại [Firebase Console](https://console.firebase.google.com/) và thêm một ứng dụng Web.
2. Trong cấu hình ứng dụng Web, chép `apiKey`, `authDomain`, `databaseURL`, `projectId` và `appId` vào `firebaseConfig` ở đầu thẻ `<script type="module">` trong [index.html](./index.html). `databaseURL` lấy trong mục Realtime Database.
3. Trong **Authentication → Sign-in method**, bật **Anonymous**.
4. Tạo **Realtime Database**. Trong mục **Rules**, dán nội dung từ [database.rules.json](./database.rules.json) rồi bấm **Publish**.
5. Đẩy dự án lên GitHub, vào Vercel chọn **Add New → Project** và import repository. Chọn **Other** nếu Vercel hỏi framework, để trống build command và bấm **Deploy**. Firebase Authentication có thể yêu cầu thêm tên miền Vercel vào danh sách **Authorized domains**.

## Chạy thử

Mở `index.html` qua hosting tĩnh hoặc máy chủ local có HTTPS/localhost. Firebase Web SDK được tải từ CDN; cần kết nối Internet.

## Lưu ý

- Đây là một phòng chat chung: ai có URL đều có thể đọc, gửi và xóa mọi tin nhắn.
- Ứng dụng tự dọn tin nhắn sau 6 giờ khi có người mở phòng chat (kiểm tra mỗi phút). Nếu không ai mở phòng, tin quá hạn sẽ được dọn khi có người vào lại.
- Mỗi trình duyệt chỉ tải 100 tin nhắn gần nhất.
- Cấu hình Firebase Web hiển thị trong HTML là bình thường; quyền truy cập được giới hạn bằng Authentication và Database Rules. Không mở quyền đọc/ghi công khai trong Rules.
