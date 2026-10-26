# CAN-Control Web

Bản web tiếng Việt của app **CAN-Control V1.29** (mini-program "CAN蓝牙"), dùng Web Bluetooth.

## Chạy
```bash
cd can-control-web
python3 -m http.server 8765
# mở http://localhost:8765 bằng Chrome / Edge
```
Web Bluetooth chỉ chạy trên `https://` hoặc `localhost`. Muốn dùng trên điện thoại thì đưa lên host có HTTPS (Vercel, GitHub Pages, Netlify…).
iPhone: Safari không hỗ trợ — dùng app trình duyệt **Bluefy**.

## Giao thức (đọc từ APK)
- BLE service `FFF0`, ghi `FFF2`, notify `FFF1`; gói tin là chuỗi hex, tối đa 20 byte mỗi lần ghi.
- Đăng nhập: `A0` + mật khẩu (ASCII hex), mặc định `0000`. `EE` hỏi thông tin thiết bị.
- `FB` = dữ liệu live (float32 little-endian từ byte 31), `FF` = toàn bộ cấu hình.
- `A6xx` bật/tắt, `A80n`+V×100+A×100 đặt điện áp/dòng, `F8xx`+giá trị×100 / `F9xx`+byte = các cài đặt.
