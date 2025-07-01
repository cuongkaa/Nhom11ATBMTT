# 📘 Gửi Báo Cáo Công Ty Qua Server Trung Gian
Một hệ thống web đảm bảo bảo mật, xác thực và toàn vẹn dữ liệu trong quá trình gửi báo cáo qua server trung gian, được xây dựng bằng Python, Flask, JavaScript và các thuật toán mã hóa như RSA, AES-GCM, SHA-512.

## 🚀 Giới thiệu chức năng và cách hoạt động của hệ thống
Hệ thống mô phỏng việc gửi báo cáo nhạy cảm từ một công ty tới một máy chủ nhận qua một server trung gian an toàn:

# 🖥️ Người gửi:
Tạo khóa RSA: Khóa công khai và khóa riêng để mã hóa và ký số.

Handshake: Gửi lời chào và khởi tạo giao tiếp an toàn với người nhận.

Ký số & trao khóa: Tạo khóa phiên AES, ký metadata bằng RSA/SHA-512, mã hóa khóa phiên bằng RSA.

Truyền báo cáo: Mã hóa nội dung bằng AES-GCM, tạo hash toàn vẹn và gửi đi kèm.

## 🛡️ Người nhận:
Giải mã khóa phiên: Dùng khóa riêng RSA để giải mã SessionKey.

Xác thực chữ ký: Kiểm tra metadata bằng chữ ký số.

Giải mã nội dung: Dùng AES-GCM để giải mã và xác thực toàn vẹn qua hash SHA-512.

Phản hồi ACK/NACK: Thông báo xác nhận hoặc lỗi đến người gửi.

## 📡 Giao tiếp:
Real-time: Sử dụng Flask SocketIO và WebSocket để gửi nhận theo thời gian thực.

Bảo mật: Kết hợp RSA (2048-bit), AES-GCM (256-bit), SHA-512, chữ ký số và hash.

## 📷 Screenshot
![Screenshot 2025-07-01 162338](https://github.com/user-attachments/assets/a017e0ad-73ee-459a-849a-e4fa9f82de5e)
![Screenshot 2025-07-01 162445](https://github.com/user-attachments/assets/d83409f1-ca0e-47ce-9e0a-4bfc315cc13a)
![Screenshot 2025-07-01 162505](https://github.com/user-attachments/assets/65053111-ce03-4759-bb7f-598e006a1497)
![Screenshot 2025-07-01 162525](https://github.com/user-attachments/assets/c1a7a72e-1a9b-4205-abcd-2ac8eadf0f36)

## 🚀Cách thức hoạt động của trang web. 
Hệ thống hoạt động theo mô hình 3 thành phần chính:
Người gửi (Sender)
Máy chủ trung gian (Server)
Người nhận (Receiver)
Mỗi thành phần có một giao diện web riêng và giao tiếp với nhau qua Socket.IO
1.	Tạo cặp khóa RSA 
Người gửi và người nhận đều tạo ra một cặp khóa RSA gồm:
Private key (bí mật)
Public key (công khai)
Public key được gửi lên server để lưu trữ và chuyển tiếp đến bên còn lại.
Mục đích: Sẵn sàng cho các bước mã hóa, xác thực và giải mã sau này.
2.	HANDSHAKE
Người gửi khởi động kết nối bằng cách gửi "Hello!" đến Người nhận.
Người nhận phản hồi "Ready!" nếu đã sẵn sàng nhận file.
Quá trình handshake được server ghi lại và giám sát theo thời gian thực.
Mục đích: Đồng bộ trạng thái và đảm bảo cả hai bên đã kết nối.
3.	Gửi khóa xác thực
Người gửi:
Tạo một Session Key (AES-256) để mã hóa dữ liệu.
Mã hóa Session Key bằng Public key của Người nhận.
Tạo một đoạn metadata gồm: tên file, thời gian gửi, transaction ID.
Ký số metadata bằng Private key của mình (đảm bảo xác thực).
Server chuyển tiếp các dữ liệu này đến Người nhận.
Mục đích: Thiết lập một khóa bí mật chung và xác thực danh tính người gửi.
Mã hóa và gửi file
Người gửi:
Mã hóa nội dung file bằng thuật toán AES-GCM (authenticated encryption).
Tính hash SHA-512 của file mã hóa (bao gồm nonce + cipher + tag).
Ký số giá trị hash bằng Private key.
Gửi gói dữ liệu gồm:
1.	Nội dung mã hóa (cipher, nonce, tag)
2.	Giá trị hash
3.	Chữ ký hash
4.	Tên file, transaction ID, dung lượng
Server chuyển tiếp gói tin đến Người nhận.
Mục đích: Đảm bảo tính bảo mật, xác thực và toàn vẹn của file.
4.	Người nhận xác thực và giải mã file
Người nhận thực hiện các bước sau:
1.	Giải mã Session Key bằng Private key của mình.
2.	Xác thực chữ ký metadata → đảm bảo không bị giả mạo.
3.	Tính lại hash SHA-512 từ file mã hóa và so sánh với hash nhận được.
4.	Xác thực chữ ký số của hash → đảm bảo nội dung đúng từ người gửi.
5.	Giải mã file bằng AES-GCM nếu các bước trên hợp lệ.
Kết quả:
Hiển thị nội dung file đã giải mã.
Cho phép tải file về nếu xác thực thành công.
Mục đích: Đảm bảo người nhận tin cậy nội dung, không bị thay đổi, đúng người gửi.

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
