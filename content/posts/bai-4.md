---
title: "Tối ưu hóa Server Đa luồng với mô hình Thread Pool"
date: 2025-12-26
draft: false
---

Một máy chủ (Server) đơn luồng chỉ có thể xử lý một yêu cầu tại một thời điểm, gây ra hiện tượng thắt nút cổ chai. Giải pháp học thuật là áp dụng mô hình **Multi-threading**. Bằng cách sử dụng `ExecutorService` trong Java, chúng ta tạo ra một tập hợp các luồng có sẵn (Thread Pool) để phục vụ đồng thời nhiều Client.

Phương pháp này giúp giảm chi phí tài nguyên khi tạo mới và hủy luồng liên tục, đồng thời tăng khả năng chịu tải (Scalability) của hệ thống.