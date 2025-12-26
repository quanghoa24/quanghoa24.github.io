---
title: "Kiến trúc RESTful API và Định dạng Trao đổi Dữ liệu JSON"
date: 2025-12-26
draft: false
---

**Representational State Transfer (REST)** là một phong cách kiến trúc phần mềm định nghĩa các ràng buộc cho việc tạo ra các dịch vụ Web. Dữ liệu thường được trao đổi dưới định dạng **JSON (JavaScript Object Notation)** nhờ tính nhẹ (Lightweight) và khả năng tương thích cao giữa các ngôn ngữ lập trình khác nhau.

Một hệ thống REST chuẩn mực phải tuân thủ tính phi trạng thái (Statelessness), nghĩa là mọi yêu cầu từ Client phải chứa đầy đủ thông tin cần thiết để Server hiểu và xử lý.