---
title: "Socket là gì? Khái niệm nền tảng về giao thức TCP/IP và UDP"
date: 2025-12-26
draft: false
image: "https://cloud-web-cms-beta.s3.cloud.cmctelecom.vn/socket_eb5681c677.jpg"
description: "Phân tích chuyên sâu về cơ chế Socket, vai trò của cổng (Port) và sự khác biệt giữa TCP/UDP Socket trong lập trình hệ thống."
---

![Socket Programming](https://cloud-web-cms-beta.s3.cloud.cmctelecom.vn/socket_eb5681c677.jpg)

Socket là một trong các khái niệm quen thuộc với lập trình viên, có cách thức hoạt động tương tự như một tập tin descriptor cấp thấp. Hiểu một cách đơn giản, Socket là điểm cuối (endpoint) của một liên kết truyền thông hai chiều giữa hai chương trình chạy trên mạng.

## 1. Bản chất kỹ thuật của Socket
Về mặt kỹ thuật, Socket là sự kết hợp giữa **Địa chỉ IP** và **Số cổng (Port number)**. 
- **Địa chỉ IP:** Xác định thiết bị trong mạng.
- **Số cổng:** Xác định ứng dụng cụ thể trên thiết bị đó.
- **Công thức:** `Socket = IP Address + Port Number`

## 2. Phân loại Socket phổ biến
Trong lập trình mạng, chúng ta chủ yếu làm việc với hai loại Socket dựa trên giao thức tầng Transport:

### 2.1. Stream Socket (Dựa trên TCP)
- **Đặc điểm:** Hướng kết nối (Connection-oriented).
- **Cơ chế:** Dữ liệu được truyền đi đảm bảo không bị mất mát, đúng thứ tự và không bị lặp lại.
- **Ứng dụng:** Web (HTTP), Email (SMTP), Truyền file (FTP).

### 2.2. Datagram Socket (Dựa trên UDP)
- **Đặc điểm:** Không hướng kết nối (Connectionless).
- **Cơ chế:** Dữ liệu được gửi đi nhanh chóng nhưng không đảm bảo độ tin cậy. Gói tin có thể bị mất hoặc đến sai thứ tự.
- **Ứng dụng:** Streaming video, Voice chat, Game online.

## 3. Quy trình hoạt động của mô hình Client-Server
Một hệ thống sử dụng Socket thường trải qua các bước sau:
1. **Socket():** Tạo một endpoint mới.
2. **Bind():** Gán địa chỉ IP và Port cho Socket (thường thực hiện ở phía Server).
3. **Listen():** Server đợi kết nối từ Client.
4. **Accept():** Chấp nhận kết nối.
5. **Connect():** Client yêu cầu kết nối tới Server.
6. **Send/Receive:** Trao đổi dữ liệu.
7. **Close():** Đóng kết nối.

## 4. Tại sao Socket lại quan trọng?
Nếu không có Socket, việc lập trình mạng sẽ trở nên cực kỳ phức tạp vì lập trình viên phải tự xử lý các tầng giao thức vật lý và logic thấp hơn. Socket cung cấp một lớp trừu tượng (Abstraction layer) giúp chúng ta chỉ cần tập trung vào việc gửi và nhận dữ liệu giữa các tiến trình.

---
*Bài viết này nằm trong chuỗi series về Lập trình mạng Java/JS chuyên sâu của Đào Quang Hòa.*