---
title: "Xử lý Bất đồng bộ trong JavaScript: Từ Callback đến Async/Await"
date: "2024-05-21T10:00:00+07:00"
draft: false
---



> ⚠️ **Lưu ý**: Bài đăng này mang tính tổng hợp kiến thức, luồng kiến trúc và đã không được cập nhật trong 3 năm. Tuy nhiên, **tư duy thiết kế realtime system với Socket.IO + Redis vẫn còn giá trị sử dụng cao**.

---

## Giới thiệu

Chào các bạn 👋  
Trong phát triển ứng dụng **realtime**, Socket.IO là một trong những lựa chọn phổ biến nhất giúp duy trì kết nối hai chiều giữa **client** và **server**.

Nhờ Socket.IO, chúng ta có thể xây dựng các ứng dụng:
- 💬 Chat realtime
- 🎮 Game online
- 🔔 Notification
- 📊 Dashboard realtime

Bài viết này tập trung vào:
- Hiểu **luồng hoạt động của Socket.IO**
- Thiết kế **hệ thống chat realtime**
- Mở rộng hệ thống bằng **Redis + Load Balancer**

---

## Socket.IO là gì?

**Socket.IO** là một thư viện hỗ trợ giao tiếp **real-time, hai chiều** giữa client (trình duyệt) và server thông qua WebSocket (và fallback cơ chế khác).

![Socket.IO Client Server](https://images.viblo.asia/c9b8b962-0a4f-4ef2-b8c2-068c2555ae0d.png)

### Kiến trúc cơ bản
- **Client**: Kết nối lên server qua Socket.IO client
- **Server**: WebSocket server (thường dùng Node.js)

Sau khi handshake thành công, client và server có thể **trao đổi dữ liệu liên tục**.

---

## Tính năng cơ bản của Socket.IO

### 1. Giao tiếp hai chiều (emit / on)

Socket.IO sử dụng hai khái niệm cốt lõi:

- `emit` → phát sự kiện
- `on` → lắng nghe sự kiện

📌 **Client và server đều có thể emit & on**

---

### 2. Các kiểu emit trong Socket.IO

Giả sử:
- Server là WebSocket Server
- Socket1, Socket2, Socket3 là các client

#### 🔹 Self Emit
Client gửi message → server → trả lại **chính client đó**

![Self Emit](https://images.viblo.asia/15e63d2d-7c1f-48b2-851a-e35428ad64c5.png)

---

#### 🔹 Broadcast Emit
Client gửi message → server → gửi cho **tất cả client khác**

![Broadcast Emit](https://images.viblo.asia/377c1c84-48fa-4425-81bd-501815540b46.png)

---

#### 🔹 Room Emit
Client gửi message → server → gửi cho **các client trong cùng room**

![Room Emit](https://images.viblo.asia/8f950b7e-7c16-40c4-89b8-abb83f39be98.png)

---

#### 🔹 SocketId Emit (Chat riêng)
Server gửi message cho **một client cụ thể**

![SocketId Emit](https://images.viblo.asia/48f10b6f-45d6-490c-a9d5-7e3efa23d47f.png)

📎 Tài liệu chi tiết:  
https://socket.io/docs/v3/broadcasting-events/

---

## Xây dựng mô hình ứng dụng chat

### 1️⃣ Quy mô nhỏ

Với hệ thống ít người dùng:

- 1 Web Server
- 1 WebSocket Server
- Client kết nối trực tiếp

![Small Scale](https://images.viblo.asia/9431ec3e-602d-4e93-bd53-30fef9a3a5c5.png)

📌 Mỗi client có một `socketId` riêng.

---

### 2️⃣ Quy mô trung bình & lớn

Vấn đề:
- Server chịu tải tối đa ~10K user
- Lượng user tăng → server quá tải → **sập**

👉 Giải pháp:
- **Load Balancer (Nginx)**
- **Redis (Pub/Sub)**

---

## Load Balancer với Nginx

Nginx phân phối request đến nhiều server Node.js theo **Round Robin**.

![Nginx Load Balance](https://images.viblo.asia/4fed4584-ea7e-4e36-b6a4-fa06950d5ce8.png)

Ví dụ:
- r1 → nodejs:8000  
- r2 → nodejs:8001  
- r3 → nodejs:8002  

---

## Vấn đề khi chỉ dùng Load Balancer

![Problem Without Redis](https://images.viblo.asia/7da08c2f-92b1-415c-8119-14813a8c2b34.png)

⚠️ Các WebSocket server **không giao tiếp được với nhau**  
→ Client ở server A không nhận được message từ client ở server B

👉 **Cần Redis hoặc dịch vụ trung gian**

---

## Redis Pub/Sub là gì?

Redis không chỉ là Key-Value store mà còn hỗ trợ **Publish / Subscribe**

- **Publish**: Đẩy message vào channel
- **Subscribe**: Nhận message từ channel

![Redis Pub Sub](https://images.viblo.asia/67c87ce0-e68e-431c-a71a-8f57bdfbb3da.png)

📌 Redis đóng vai trò **message broker**

---

## Kiến trúc tổng thể Socket.IO + Redis

![Total Architecture](https://images.viblo.asia/c16ce001-ebe6-4529-bf24-901410543261.png)

### Luồng hoạt động

1. Client connect WebSocket
2. Server WebSocket subscribe Redis channel
3. Redis publish message
4. Tất cả WebSocket server nhận message
5. Emit xuống client tương ứng

📎 Tham khảo:
https://socket.io/docs/v3/using-multiple-nodes/

---

## Ứng dụng với Laravel Broadcasting

Trong Laravel:

- Redis / Pusher làm broker
- `laravel-echo-server` dùng Socket.IO
- `laravel-echo` dùng cho client JS

📎 Docs:
https://laravel.com/docs/8.x/broadcasting

📌 Dù Node.js hay PHP, **luồng kiến trúc là như nhau**

---

## Kết luận

- Socket.IO giúp xây dựng realtime application hiệu quả
- Redis Pub/Sub giải quyết bài toán **scale nhiều WebSocket server**
- Kiến trúc này phù hợp cho:
  - Chat app
  - Notification system
  - Realtime dashboard

👉 Hiểu **luồng kiến trúc** quan trọng hơn việc chỉ biết code.

---

🚀 **Bài tiếp theo gợi ý**:
- So sánh Socket.IO vs WebSocket thuần
- Redis Streams vs Pub/Sub
- Realtime system với Kafka
