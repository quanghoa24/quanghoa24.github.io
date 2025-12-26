---
title: "Java (Backend) với JavaScript (Real-time)"
date: 2025-12-26
draft: false
---

![Fetch API là gì](https://interdata.vn/blog/wp-content/uploads/2025/05/API-Fetch-la-gi.jpg)

Trong phát triển web hiện đại, việc tương tác với máy chủ để gửi và nhận dữ liệu là cốt lõi của mọi ứng dụng. **Fetch API**, một công nghệ mạnh mẽ của JavaScript, đã trở thành giải pháp tiêu chuẩn cho tác vụ này, mang lại hiệu suất vượt trội và cú pháp minh bạch.

Đọc bài viết để hiểu **Fetch API là gì, cách hoạt động, lợi ích và những ứng dụng thực tế**, giúp lập trình viên từ mọi cấp độ dễ dàng nắm bắt.

---

## Fetch là gì?

### Fetch API trong JavaScript là gì?

**Fetch API** là một giao diện hiện đại của JavaScript dùng để thực hiện các yêu cầu HTTP như **GET, POST, PUT, DELETE** và xử lý phản hồi từ máy chủ một cách linh hoạt ngay trong trình duyệt.

Fetch API được thiết kế để **thay thế XMLHttpRequest (XHR)**, mang lại cú pháp gọn gàng hơn nhờ sử dụng **Promise**, giúp việc xử lý các tác vụ bất đồng bộ trở nên trực quan và dễ bảo trì hơn.

---

## API Fetch là gì?

Khi sử dụng Fetch API, bạn chỉ cần gọi hàm `fetch()` với URL mong muốn, kèm theo các tùy chọn như:

- `method`
- `headers`
- `body`
- `mode`, `credentials`, …

Hàm `fetch()` **trả về một Promise**, khi hoàn thành sẽ cung cấp đối tượng **Response** để kiểm tra trạng thái và trích xuất dữ liệu (JSON, text, blob,…).

Fetch API cũng tích hợp tốt với:
- **CORS**
- **Service Workers**
- **Progressive Web Apps (PWA)**

---

## API Fetch hoạt động như thế nào?

Fetch API sử dụng cú pháp **dựa trên Promise**, giúp xử lý bất đồng bộ rõ ràng hơn.

### Ví dụ gọi API bằng Fetch

```javascript
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Lỗi:', error));
