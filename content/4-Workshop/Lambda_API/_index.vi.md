---
title: "Lambda & API Gateway"
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

Trong phần này, chúng ta tạo các Lambda function và kết nối chúng với API Gateway.

## Những gì sẽ xây dựng

| Route         | Lambda             | Yêu cầu xác thực |
| ------------- | ------------------ | ---------------- |
| `POST /login` | `loginFunction`    | Không            |
| `GET /songs`  | `getSongsFunction` | Có (JWT)         |

## Các bước

1. [Tạo Lambda Functions](Lambda/)
2. [Cài đặt API Gateway](API-Gateway/)
3. [Kết nối Lambda với API Gateway](API_Lambda/)
