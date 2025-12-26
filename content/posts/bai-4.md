---
title: "Tối ưu hóa Server Đa luồng với mô hình Thread Pool"
date: 2025-05-18
draft: false
---

## Tối ưu hóa Server Đa luồng với mô hình Thread Pool

![Thread Pool Overview](https://images.viblo.asia/efdf086b-41d8-4d60-b6e8-a94ac6c51db9.png)

Trong các hệ thống **server hiện đại**, việc xử lý đồng thời nhiều yêu cầu từ client là yêu cầu bắt buộc. Nếu mỗi request tạo một luồng (thread) mới, server rất dễ rơi vào tình trạng **quá tải tài nguyên**, giảm hiệu năng và thậm chí bị treo.

Mô hình **Thread Pool** ra đời nhằm giải quyết vấn đề này bằng cách **tái sử dụng các luồng**, giúp server hoạt động ổn định và hiệu quả hơn.

---

## Khái niệm Thread Pool

**Thread Pool** là một tập hợp các **thread được tạo sẵn**, luôn ở trạng thái chờ để thực thi các tác vụ (task).

Thay vì:
- Request → tạo thread → xử lý → hủy thread  

Thread Pool hoạt động như sau:
- Request → đưa vào **hàng đợi (BlockingQueue)**
- Thread rảnh → lấy task → xử lý
- Xử lý xong → quay về pool

---

## Vì sao không nên tạo thread liên tục?

Giả sử một Web Server:
- Mỗi request xử lý mất 0.5s
- 100 request đến cùng lúc
- 10 triệu request / tháng

👉 Nếu mỗi request tạo một thread mới:
- Chi phí tạo thread rất lớn
- Tốn bộ nhớ stack
- Giảm hiệu năng
- Dễ gây **OutOfMemoryError**

➡️ **Thread Pool** giúp giải quyết triệt để vấn đề này.

---

## Cơ chế hoạt động của Thread Pool

![Thread Pool Queue](https://images.viblo.asia/ef5de1ba-d8c6-480a-866a-1a9d4aca22c4.png)

Cấu trúc cơ bản gồm:
- **Thread Pool**: tập các thread cố định
- **BlockingQueue**: hàng đợi các task
- **Worker Thread**: lấy task ra xử lý

Khi số request > số thread:
- Request sẽ **xếp hàng**
- Đợi đến khi có thread rảnh

---

## Executor trong Java là gì?

**Executor** là một thành phần thuộc package `java.util.concurrent`, chịu trách nhiệm:
- Quản lý vòng đời thread
- Lập lịch thực thi task
- Tách biệt logic xử lý và quản lý thread

👉 Executor đóng vai trò như **wrapper** cho Thread Pool, giúp lập trình viên:
- Không cần tự tạo thread
- Không cần tự quản lý queue
- Tập trung vào logic nghiệp vụ

---

## Các loại Thread Pool trong Java

Java cung cấp lớp tiện ích **Executors** để tạo Thread Pool:

### 🔹 Single Thread Executor
```java
Executors.newSingleThreadExecutor();
