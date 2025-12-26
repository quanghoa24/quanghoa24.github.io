---
title: "UDP Socket: Phân tích Hiệu năng và Ứng dụng Thời gian thực"
date: 2025-12-26
draft: false
---

Ngược lại với TCP, **User Datagram Protocol (UDP)** là giao thức phi kết nối (Connectionless), ưu tiên tối thiểu hóa độ trễ (Latency) thay vì đảm bảo thứ tự gói tin. Sử dụng `DatagramSocket` và `DatagramPacket` trong Java cho phép lập trình viên đóng gói dữ liệu vào các đơn vị độc lập. 

Cơ chế này đặc biệt tối ưu cho các hệ thống Real-time như truyền phát video (Streaming) hoặc VoIP, nơi việc mất mát một tỉ lệ nhỏ dữ liệu có thể chấp nhận được để duy trì tính liên tục của dòng dữ liệu.