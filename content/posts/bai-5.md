---
title: "Xử lý Bất đồng bộ trong JavaScript: Từ Callback đến Async/Await"
date: 2025-05-19
draft: false
---

## Giới thiệu

![Asynchronous JavaScript](https://images.viblo.asia/a4c460bb-d717-48b2-8d2b-2265beab6dff.png)

JavaScript là ngôn ngữ **đơn luồng (single-threaded)** nhưng lại có khả năng xử lý các tác vụ **bất đồng bộ (asynchronous)** rất hiệu quả.  
Nhờ cơ chế này, JavaScript có thể xử lý các công việc tốn thời gian như:

- Gọi API
- Đọc / ghi file
- Xử lý sự kiện người dùng
- Timer, animation

mà **không làm treo chương trình**.

---

## Bất đồng bộ là gì?

![Blocking vs Non-blocking](https://images.viblo.asia/c4dcb16e-458c-4e18-a194-4b4287c81333.png)

**Bất đồng bộ** là cơ chế cho phép một tác vụ chạy nền, trong khi luồng chính vẫn tiếp tục thực thi các công việc khác.

👉 Trái ngược với **đồng bộ (synchronous)**, nơi chương trình phải chờ tác vụ hoàn thành trước khi chạy tiếp.

---

## Callback – Cách tiếp cận truyền thống

![Callback Function](https://images.viblo.asia/827717a9-487a-45c1-8665-6888fe258f2f.png)

### Ví dụ Callback

```js
function fetchData(callback) {
  setTimeout(() => {
    callback("Dữ liệu đã tải xong");
  }, 1000);
}

fetchData(data => {
  console.log(data);
});
