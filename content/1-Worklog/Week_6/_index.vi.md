---
title: "Worklog Tuần 6"
weight: 6
chapter: false
pre: " <b> 1.6 </b> "
---

### 📌 Mục tiêu

- Xây dựng các API phục vụ chức năng quản lý (Người dùng, Nội dung, Nghệ sĩ)
- Triển khai Lambda function xử lý logic backend
- Kết nối API Gateway với Lambda
- Thiết lập các phương thức gọi API cho FE.

---

### 🛠 Công việc thực hiện

| Công việc                            | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                                                              |
| ------------------------------------ | ------------ | --------------- | ------------------------------------------------------------------------------- |
| Thiết lập các API quản lý người dùng | 13/04/2026   | 15/04/2026      | https://docs.aws.amazon.com/lambda <br/> https://docs.aws.amazon.com/apigateway |
| Thiết lập các API quản lý nội dung   | 15/04/2026   | 16/04/2026      | https://docs.aws.amazon.com/lambda <br/> https://docs.aws.amazon.com/apigateway |
| Thiết lập các API quản lý nghệ sĩ    | 16/04/2026   | 17/04/2026      | https://docs.aws.amazon.com/lambda <br/> https://docs.aws.amazon.com/apigateway |

---

### ✅ Kết quả nhận được

- Xây dựng được hệ thống API cơ bản:
  - API quản lý User
  - API xử lý báo cáo nội dung
  - API quản lý Artist và yêu cầu nâng cấp
  - API quản lý Album

- Triển khai Lambda function:
  - Xử lý logic nghiệp vụ cho từng module
  - Kết nối với DynamoDB để lưu trữ dữ liệu

- Thiết lập API Gateway:
  - Tạo và cấu hình các endpoint RESTful
  - Liên kết Lambda với từng API tương ứng

- Chuẩn hóa dữ liệu hệ thống:
  - Thiết kế request/response theo JSON thống nhất
  - Đảm bảo dễ tích hợp với frontend

---
