---
title: "Worklog Tuần 3"
weight: 3
chapter: false
pre: " <b> 1.3 </b> "
---

### 📌 Mục tiêu

- Lựa chọn công nghệ và ngôn ngữ phát triển cho hệ thống
- Thiết lập môi trường phát triển (frontend & backend)
- Bắt đầu triển khai các dịch vụ AWS đã thiết kế ở tuần 2
- Chuẩn bị nền tảng cho việc phát triển tính năng

---

### 🛠 Công việc thực hiện

| Công việc                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| ------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------ |
| Lựa chọn công nghệ: React (Frontend), Node.js (Backend), AWS SAM                                                                            | 23/03/2026   | 23/03/2026      |                    |
| Phân tích lý do lựa chọn công nghệ (hiệu năng, cộng đồng, phù hợp serverless)                                                               | 23/03/2026   | 23/03/2026      |                    |
| Setup GitHub repository và cấu trúc project (frontend/backend)                                                                              | 23/03/2026   | 24/03/2026      |                    |
| Khởi tạo dự án React và cài đặt TailwindCSS                                                                                                 | 24/03/2026   | 25/03/2026      |                    |
| Khởi tạo backend với AWS SAM Template                                                                                                       | 25/03/2026   | 26/03/2026      |                    |
| Tạo và cấu hình S3 bucket (lưu trữ file audio)                                                                                              | 26/03/2026   | 26/03/2026      |                    |
| Tạo DynamoDB tables và lên các quy định Key cho các thực thể trong dự án (User,Song,Album,History,Playlist,Artist và một thực thể quan hệ ) | 26/03/2026   | 27/03/2026      |                    |
| Tạo Lambda function cơ bản (test API)                                                                                                       | 27/03/2026   | 28/03/2026      |                    |
| Kết nối Lambda với API Gateway (test endpoint)                                                                                              | 28/03/2026   | 28/03/2026      |                    |

---

### ✅ Kết quả nhận được

- Lựa chọn được công nghệ phù hợp với mô hình serverless:
  - React và Tailwind cho frontend giúp xây dựng UI linh hoạt
  - Node.js phù hợp với AWS Lambda
  - AWS SAM hỗ trợ triển khai backend nhanh chóng

- Thiết lập hoàn chỉnh môi trường phát triển:
  - Quản lý source code bằng GitHub
  - Tách biệt rõ frontend và backend
  - Cấu trúc project rõ ràng, dễ mở rộng

- Khởi tạo thành công các dịch vụ AWS cốt lõi:
  - S3 bucket để lưu trữ file audio
  - DynamoDB tables để lưu trữ dữ liệu
    -API Gateway và Lambda để lưu trữ các phương thức xử lý logic, API.

- Hiểu rõ quy trình thiết lập dịch vụ trên AWS:
  - Cấu hình quyền truy cập (IAM roles, policies)
  - Kết nối giữa các dịch vụ (Lambda, DynamoDB, API Gateway, S3)

- Xây dựng được backend cơ bản:
  - Tạo Lambda function đầu tiên
  - Kết nối API Gateway để expose endpoint
  - Test thành công request/response
