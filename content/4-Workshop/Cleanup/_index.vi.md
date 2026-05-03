---
title: "Dọn dẹp tài nguyên"
weight: 5
chapter: false
pre: " <b> 4.5 </b> "
---

{{% notice warning %}}
Xóa tất cả tài nguyên sau khi hoàn thành workshop để tránh bị tính phí ngoài ý muốn.
{{% /notice %}}

Xóa tài nguyên theo thứ tự sau để tránh lỗi phụ thuộc.

---

## 1. Xóa API Gateway

1. Vào **API Gateway Console** → **APIs**
2. Chọn `workshop-api` → **Actions** → **Delete**
3. Xác nhận xóa

---

## 2. Xóa Lambda functions

1. Vào **Lambda Console** → **Functions**
2. Chọn `loginFunction` → **Actions** → **Delete** → xác nhận
3. Chọn `getSongsFunction` → **Actions** → **Delete** → xác nhận

---

## 3. Xóa DynamoDB table

1. Vào **DynamoDB Console** → **Tables**
2. Chọn `songs` → **Delete** → gõ `confirm` → **Delete**

---

## 4. Xóa Cognito User Pool

1. Vào **Cognito Console** → **User pools**
2. Chọn `workshop-pool` → **Delete** → gõ tên pool để xác nhận → **Delete**

---

## 5. Xóa IAM Role

1. Vào **IAM Console** → **Roles**
2. Tìm `lambda-workshop-role` → chọn → **Delete** → xác nhận

---

## 6. Xóa CloudWatch Log Groups (tùy chọn)

Lambda tự động tạo log group. Chi phí thấp nhưng bạn có thể dọn sạch:

1. Vào **CloudWatch Console** → **Log groups**
2. Tìm `/aws/lambda/loginFunction` → chọn → **Actions** → **Delete log group**
3. Lặp lại với `/aws/lambda/getSongsFunction`

---

## Kiểm tra lại

Sau khi xóa, xác nhận trong từng console rằng tài nguyên đã biến mất:

- API Gateway → không còn `workshop-api`
- Lambda → không còn `loginFunction` hay `getSongsFunction`
- DynamoDB → không còn table `songs`
- Cognito → không còn `workshop-pool`
- IAM → không còn `lambda-workshop-role`
