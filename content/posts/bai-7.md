---
title: "WebSocket và Socket.io: Giải pháp Giao tiếp Song công Toàn phần"
date: 2025-12-26
draft: false
---

Giao thức **WebSocket** thiết lập một kênh giao tiếp song công (Full-duplex) trên một kết nối TCP duy nhất, cho phép Server chủ động đẩy dữ liệu về phía Client (Server-Sent Events). **Socket.io** là một thư viện bậc cao cung cấp các tính năng bổ sung như tự động kết nối lại (Auto-reconnect) và phát tin quảng bá (Broadcasting).

Đây là công nghệ cốt lõi cho các hệ thống Chat trực tuyến và các bảng điều khiển tài chính yêu cầu cập nhật dữ liệu liên tục theo mili giây.