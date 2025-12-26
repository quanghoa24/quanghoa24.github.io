---
title: "Khái niệm Socket & Kiến trúc Client-Server: Nền tảng Giao tiếp Mạng"
date: 2025-12-26
draft: false
---

Trong bối cảnh hệ thống phân tán, **Socket** đóng vai trò là một trừu tượng hóa phần mềm (Software Abstraction), tạo thành một điểm cuối (Endpoint) cho giao diện lập trình ứng dụng (API) giữa các tiến trình giao tiếp. Một Socket được định danh bởi bộ ngũ (5-tuple) bao gồm: giao thức, địa chỉ IP nguồn/đích và số hiệu cổng (Port) nguồn/đích.

Kiến trúc **Client-Server** thiết lập một mô hình bất đối xứng:
- **Server:** Duy trì trạng thái lắng nghe (Listen) trên một cổng xác định, sẵn sàng tiếp nhận yêu cầu từ tầng truyền tải.
- **Client:** Khởi tạo yêu cầu kết nối thông qua tiến trình định danh từ xa.