---
title: "Worklog Tuần 2"
weight: 2
chapter: false
pre: " <b> 1.2 </b> "
---

### 📌 Mục tiêu

- Hiểu các dịch vụ cốt lõi của AWS: S3, DynamoDB, API Gateway, Lambda, Cognito
- Thiết kế kiến trúc hệ thống theo mô hình serverless
- Thiết kế cơ sở dữ liệu NoSQL phù hợp với bài toán
- Phân tích và mô hình hóa các yêu cầu chức năng và phi chức năng
- Lựa chọn các dịch vụ và cấu hình tài nguyên phù hợp, tối ưu chi phí (Free Tier)

---

### 🛠 Công việc thực hiện

| Công việc                                                                           | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                     |
| ----------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------- |
| Tìm hiểu Amazon S3 (cách lưu trữ file audio, cơ chế object storage, quyền truy cập) | 16/03/2026   | 17/03/2026      | https://docs.aws.amazon.com/s3         |
| Tìm hiểu DynamoDB (NoSQL, partition key, sort key, thiết kế bảng)                   | 17/03/2026   | 18/03/2026      | https://docs.aws.amazon.com/dynamodb   |
| Tìm hiểu AWS Lambda và mô hình serverless                                           | 18/03/2026   | 19/03/2026      | https://docs.aws.amazon.com/lambda     |
| Tìm hiểu API Gateway (REST API, routing request)                                    | 19/03/2026   | 19/03/2026      | https://docs.aws.amazon.com/apigateway |
| Tìm hiểu AWS Cognito (Authentication & Authorization)                               | 19/03/2026   | 20/03/2026      | https://docs.aws.amazon.com/cognito    |
| Phân tích yêu cầu hệ thống (User, Song, Playlist, Streaming)                        | 20/03/2026   | 20/03/2026      |                                        |
| Thiết kế Database Schema (User, Song, Playlist)                                     | 20/03/2026   | 20/03/2026      |                                        |
| Thiết kế kiến trúc hệ thống (S3 + Lambda + API Gateway + DynamoDB + Cognito)        | 20/03/2026   | 20/03/2026      |                                        |
| Xác định tài nguyên AWS phù hợp với Free Tier                                       | 20/03/2026   | 20/03/2026      |                                        |

---

### ✅ Kết quả nhận được

- Hiểu rõ vai trò và cách hoạt động của từng dịch vụ AWS cốt lõi:
  - S3: lưu trữ file audio dạng object, hỗ trợ truy cập qua URL
  - DynamoDB: lưu trữ dữ liệu dạng NoSQL với hiệu năng cao
  - Lambda: xử lý logic backend theo mô hình serverless
  - API Gateway: trung gian nhận request từ client và gọi Lambda
  - Cognito: quản lý người dùng, xác thực và phân quyền

- Nắm được mô hình kiến trúc serverless và ưu điểm:
  - Không cần quản lý server
  - Tự động scale
  - Tối ưu chi phí theo mức sử dụng

- Thiết kế được kiến trúc tổng thể của hệ thống:
  - Frontend → API Gateway → Lambda → DynamoDB
  - File audio được lưu trữ và truy xuất từ S3
  - Authentication được xử lý bởi Cognito

- Xây dựng được Database Schema NoSQL:
  - Bảng User (userId, email, metadata)
  - Bảng Song (songId, title, artist, fileUrl)
  - Bảng Playlist (playlistId, userId, listSongIds)

- Hiểu cách thiết kế dữ liệu theo hướng truy vấn (query-first design) trong NoSQL

- Phân tích và xác định được:
  - Yêu cầu chức năng: đăng ký, đăng nhập, nghe nhạc, tạo playlist
  - Yêu cầu phi chức năng: hiệu năng, bảo mật, khả năng mở rộng

- Lựa chọn được các dịch vụ AWS phù hợp với Free Tier:
  - S3 (lưu trữ miễn phí giới hạn)
  - DynamoDB (free read/write capacity)
  - Lambda (free request/tháng)
  - API Gateway (giới hạn miễn phí)

- Hình thành tư duy thiết kế hệ thống cloud theo hướng:
  - Tách biệt frontend – backend
  - Sử dụng dịch vụ managed
  - Tối ưu chi phí ngay từ giai đoạn thiết kế
