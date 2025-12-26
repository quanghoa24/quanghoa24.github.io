---
title: "Giao thức TCP và Cơ chế Truyền tải Tin cậy trong Java"
date: 2025-12-26
draft: false
---

Giao thức **Transmission Control Protocol (TCP)** đảm bảo tính toàn vẹn dữ liệu thông qua cơ chế bắt tay ba bước (Three-way Handshake) và kiểm soát luồng (Flow Control). Trong ngôn ngữ Java, lớp `ServerSocket` và `Socket` cung cấp các luồng vào/ra (InputStream/OutputStream) để thực thi việc truyền tin hướng kết nối.

Điểm cốt lõi trong lập trình TCP Java là việc quản lý ngoại lệ (Exception Handling) và đóng tài nguyên hệ thống sau khi phiên làm việc (Session) kết thúc để tránh hiện tượng rò rỉ bộ nhớ.