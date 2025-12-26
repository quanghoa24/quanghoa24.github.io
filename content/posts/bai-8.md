+++
title = "Tìm Hiểu RESTful API và Các Tiêu Chuẩn Viết API Hiệu Quả"
date = 2024-05-22T10:00:00+07:00
draft = false
+++


## Giới thiệu RESTful API

RESTful API (Representational State Transfer API) là một phong cách kiến trúc và phương pháp tiếp cận được sử dụng rộng rãi trong việc xây dựng các dịch vụ web. RESTful API dựa trên giao thức HTTP để thực hiện các hoạt động CRUD (Create, Read, Update, Delete) trên các tài nguyên.

Sự phổ biến của RESTful API đến từ:
- Tính đơn giản
- Dễ hiểu
- Khả năng mở rộng cao
- Phù hợp với các hệ thống phân tán hiện đại

![RESTful API Overview](https://images.viblo.asia/5442e738-c456-4f58-a416-28765f6f25c2.png)

---

## Nguyên tắc cơ bản của RESTful API

RESTful API tuân theo **6 nguyên tắc cốt lõi** nhằm định hình cách giao tiếp giữa client và server.

### 1. Client – Server (Máy khách – Máy chủ)

Client chịu trách nhiệm giao diện và trải nghiệm người dùng, trong khi server quản lý dữ liệu và logic nghiệp vụ. Việc tách biệt này giúp hệ thống dễ bảo trì và mở rộng.

---

### 2. Stateless (Không trạng thái)

Mỗi request từ client phải chứa đầy đủ thông tin để server xử lý. Server **không lưu trạng thái** của client giữa các request, giúp tăng khả năng mở rộng và giảm phụ thuộc.

---

### 3. Cacheable (Có thể lưu bộ nhớ đệm)

Response cần chỉ rõ có thể cache hay không, giúp:
- Giảm tải server
- Tăng tốc độ phản hồi cho client

---

### 4. Uniform Interface (Giao diện đồng nhất)

- Tài nguyên được truy cập qua URL duy nhất
- Dữ liệu biểu diễn bằng định dạng chuẩn (JSON, XML)
- Giao diện nhất quán giúp API dễ học và dễ sử dụng

---

### 5. Layered System (Hệ thống phân lớp)

REST cho phép nhiều lớp trung gian như:
- Load Balancer
- Gateway
- Authentication Service

Client không cần biết request đang đi qua bao nhiêu lớp.

---

### 6. Code on Demand (Tùy chọn)

Server có thể gửi mã thực thi (ví dụ JavaScript) cho client để mở rộng chức năng, tuy nhiên nguyên tắc này **không bắt buộc**.

---

## Các phương thức HTTP thường dùng trong RESTful API

### 1. GET
Truy vấn dữ liệu  
Ví dụ:
