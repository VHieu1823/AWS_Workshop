---
title: "Kiểm tra kết nối"
weight: 3
chapter: false
pre: " <b> 4.3.3 </b> "
---

Tại bước này, cả hai Lambda function đã được kết nối với API Gateway. Hãy kiểm tra nhanh trước khi chuyển sang phần test đầy đủ.

---

## Kiểm tra integration

1. Trong API Gateway, nhấn vào `/login` → **POST** → **Integration Request**
2. Xác nhận **Lambda Function** hiển thị `loginFunction`

3. Nhấn vào `/songs` → **GET** → **Integration Request**
4. Xác nhận **Lambda Function** hiển thị `getSongsFunction`

5. Nhấn vào `/songs` → **GET** → **Method Request**
6. Xác nhận **Authorization** hiển thị `CognitoAuthorizer`
   ![Deploy API](/AWS_Workshop/images/img/inter1.png)
   ![Deploy API](/AWS_Workshop/images/img/inter2.png)
   ![Deploy API](/AWS_Workshop/images/img/inter3.png)

---

## Test nhanh từ console

API Gateway có công cụ test tích hợp sẵn.

### Test POST /login

1. Nhấn `/login` → **POST** → **TEST** (biểu tượng tia sét)
2. Trong **Request Body**, dán vào:

```json
{
  "email": "test@example.com",
  "password": "Test@12345"
}
```

3. Nhấn **Test**
4. Kết quả mong đợi: `Status: 200` với `idToken`, `accessToken`, `refreshToken` trong response body

### Test GET /songs không có token

1. Nhấn `/songs` → **GET** → **TEST**
2. Để trống tất cả → **Test**
3. Kết quả mong đợi: `Status: 401` — authorizer chặn request

### Test GET /songs có token

1. Lấy token từ bước test login ở trên — sao chép `idToken`
2. Nhấn `/songs` → **GET** → **TEST**
3. Trong **Headers**, thêm:
   ```
   Authorization: <dán idToken vào đây>
   ```
4. Nhấn **Test**
5. Kết quả mong đợi: `Status: 200` với danh sách bài hát

Nếu cả ba test đều pass, cấu hình đã đúng. Chuyển sang phần Kiểm thử để test end-to-end với HTTP client thực tế.
