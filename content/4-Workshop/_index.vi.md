---
title: "Workshop"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

# Xây dựng Serverless API với API Gateway, Lambda và Cognito

## Tổng quan

Trong workshop này, bạn sẽ xây dựng một REST API serverless đơn giản trên AWS để xử lý xác thực người dùng và quản lý bài hát. Toàn bộ thao tác thực hiện qua AWS Management Console — không cần framework hay CLI ngoài việc viết code cho Lambda function.

Kết thúc workshop, bạn sẽ có một API hoạt động được với các chức năng:

- Xác thực người dùng qua **Amazon Cognito**
- Bảo vệ route bằng **JWT Authorizer** trên API Gateway
- Lưu trữ và truy vấn dữ liệu từ **DynamoDB**
- Xử lý logic nghiệp vụ trên **AWS Lambda**

---

## Kiến trúc

```
Client → API Gateway → Cognito JWT Authorizer → Lambda → DynamoDB
```

- **Route công khai:** `POST /login` — ai cũng có thể gọi
- **Route được bảo vệ:** `GET /songs` — yêu cầu JWT token hợp lệ

---

## Yêu cầu

- Tài khoản AWS (Free Tier là đủ)
- Hiểu cơ bản về REST API (GET, POST, JSON là gì)
- Không cần kinh nghiệm AWS trước đó

---

## Nội dung

1. [Giới thiệu](Introduction/)
2. [Chuẩn bị](Prerequiste/)
3. [Lambda & API Gateway](Lambda_API/)
4. [Kiểm thử](Testing/)
5. [Dọn dẹp tài nguyên](Cleanup/)
