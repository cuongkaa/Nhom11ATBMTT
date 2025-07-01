#📘 Gửi Báo Cáo Công Ty Qua Server Trung Gian
Một hệ thống web đảm bảo bảo mật, xác thực và toàn vẹn dữ liệu trong quá trình gửi báo cáo qua server trung gian, được xây dựng bằng Python, Flask, JavaScript và các thuật toán mã hóa như RSA, AES-GCM, SHA-512.

##🚀 Giới thiệu chức năng và cách hoạt động của hệ thống
Hệ thống mô phỏng việc gửi báo cáo nhạy cảm từ một công ty tới một máy chủ nhận qua một server trung gian an toàn:

🖥️ Người gửi:
Tạo khóa RSA: Khóa công khai và khóa riêng để mã hóa và ký số.

Handshake: Gửi lời chào và khởi tạo giao tiếp an toàn với người nhận.

Ký số & trao khóa: Tạo khóa phiên AES, ký metadata bằng RSA/SHA-512, mã hóa khóa phiên bằng RSA.

Truyền báo cáo: Mã hóa nội dung bằng AES-GCM, tạo hash toàn vẹn và gửi đi kèm.

🛡️ Người nhận:
Giải mã khóa phiên: Dùng khóa riêng RSA để giải mã SessionKey.

Xác thực chữ ký: Kiểm tra metadata bằng chữ ký số.

Giải mã nội dung: Dùng AES-GCM để giải mã và xác thực toàn vẹn qua hash SHA-512.

Phản hồi ACK/NACK: Thông báo xác nhận hoặc lỗi đến người gửi.

📡 Giao tiếp:
Real-time: Sử dụng Flask SocketIO và WebSocket để gửi nhận theo thời gian thực.

Bảo mật: Kết hợp RSA (2048-bit), AES-GCM (256-bit), SHA-512, chữ ký số và hash.
## 🚀 Demo

## 📷 Screenshot
![Screenshot 2025-07-01 162338](https://github.com/user-attachments/assets/a017e0ad-73ee-459a-849a-e4fa9f82de5e)
![Screenshot 2025-07-01 162445](https://github.com/user-attachments/assets/d83409f1-ca0e-47ce-9e0a-4bfc315cc13a)
![Screenshot 2025-07-01 162505](https://github.com/user-attachments/assets/65053111-ce03-4759-bb7f-598e006a1497)
![Screenshot 2025-07-01 162525](https://github.com/user-attachments/assets/c1a7a72e-1a9b-4205-abcd-2ac8eadf0f36)

## 📁 Cấu trúc dự án

```bash
.
├── main.py
├── templates/
│   └── index.html
│   └── receiver.html
│   └── sender.html
│   └── server.html  
└── README.md
