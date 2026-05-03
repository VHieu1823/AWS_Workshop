---
title: "Giới thiệu"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

## Chúng ta sẽ xây dựng gì?

Một REST API serverless đơn giản cho ứng dụng nhạc. Người dùng có thể đăng nhập và lấy danh sách bài hát. API chạy hoàn toàn trên các dịch vụ managed của AWS — không cần quản lý server.

---

## Các dịch vụ sử dụng

### Amazon Cognito

Quản lý tài khoản người dùng. Người dùng đăng ký và đăng nhập qua Cognito, Cognito sẽ cấp một **JWT token** (một chuỗi ký tự đã được ký, xác nhận danh tính của bạn). Token này được dùng để bảo vệ các route API.

### AWS Lambda

Chạy code mà không cần server. Mỗi endpoint API tương ứng với một Lambda function. Lambda chỉ chạy khi có request đến, nên bạn chỉ trả tiền cho lượng sử dụng thực tế.

### Amazon API Gateway

Cổng vào của API. Nhận HTTP request từ client và chuyển đến đúng Lambda function. API Gateway cũng kiểm tra JWT token trước khi chuyển request đến Lambda.

### Amazon DynamoDB

Cơ sở dữ liệu NoSQL. Nhanh, serverless và tự động mở rộng. Dùng để lưu dữ liệu bài hát.

![Sơ đồ kiến trúc](/AWS_Workshop/images/img/workshop_architec.png)

---

## Luồng xử lý request

**Đăng nhập (công khai):**

```
Client → POST /login → API Gateway → Lambda (login) → Cognito → trả về JWT token
```

**Lấy danh sách bài hát (được bảo vệ):**

```
Client → GET /songs → API Gateway → [kiểm tra JWT] → Lambda (getSongs) → DynamoDB → trả về danh sách
```

Nếu JWT token thiếu hoặc không hợp lệ, API Gateway từ chối request với lỗi `401 Unauthorized` trước khi request đến Lambda.

---

## Các bước thực hiện

1. Tạo DynamoDB table và Cognito user pool
2. Viết hai Lambda function: `login` và `getSongs`
3. Tạo API Gateway với hai route
4. Gắn Cognito JWT Authorizer để bảo vệ `GET /songs`
5. Kiểm thử end-to-end
6. Dọn dẹp tài nguyên
