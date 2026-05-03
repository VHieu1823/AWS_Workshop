---
title: "Kiểm thử"
weight: 4
chapter: false
pre: " <b> 4.4 </b> "
---

Bây giờ chúng ta test toàn bộ flow bằng HTTP request thực tế. Bạn có thể dùng **Postman**, **curl**, hoặc PowerShell.

Đặt Invoke URL của bạn vào biến:

```
BASE_URL = https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev
```

---

## Test 1: Đăng nhập đúng thông tin

**PowerShell:**

```powershell
Invoke-RestMethod -Method POST `
  -Uri "$BASE_URL/login" `
  -ContentType "application/json" `
  -Body (@{ email="test@example.com"; password="Test@12345" } | ConvertTo-Json)
```

**curl:**

```bash
curl -X POST "$BASE_URL/login" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"Test@12345"}'
```

Kết quả mong đợi:

```json
{
  "accessToken": "...",
  "idToken": "eyJraWQ...",
  "refreshToken": "..."
}
```

Sao chép `idToken` — bạn sẽ dùng nó ở các test tiếp theo.

![Đăng nhập thành công](/images/img/RQ1.png)

---

## Test 2: Lấy danh sách bài hát với token hợp lệ

**PowerShell:**

```powershell
Invoke-RestMethod -Method GET `
  -Uri "$BASE_URL/songs" `
  -Headers @{ Authorization = "<dán idToken vào đây>" }
```

**curl:**

```bash
curl -X GET "$BASE_URL/songs" \
  -H "Authorization: <dán idToken vào đây>"
```

Kết quả mong đợi:

```json
{
  "songs": [
    {
      "songId": "1",
      "title": "Lạc Trôi",
      "artist": "Sơn Tùng M-TP",
      "genre": "vpop"
    }
  ],
  "count": 1
}
```

![Lấy bài hát thành công](/images/img/Result.png)

---

## Test 3: Lấy bài hát không có token

**PowerShell:**

```powershell
Invoke-RestMethod -Method GET -Uri "$BASE_URL/songs"
```

Kết quả mong đợi: `401 Unauthorized`

Request bị API Gateway từ chối trước khi đến Lambda.

![Không có token](/images/img/Result2.png)

---

## Test 4: Đăng nhập sai mật khẩu

**PowerShell:**

```powershell
Invoke-RestMethod -Method POST `
  -Uri "$BASE_URL/login" `
  -ContentType "application/json" `
  -Body (@{ email="test@example.com"; password="saimatkhau" } | ConvertTo-Json)
```

Kết quả mong đợi: `401` với message `"Email hoặc mật khẩu không đúng"`

![Sai mật khẩu](/images/img/Result3.png)

---

## Kiểm tra CloudWatch logs

Nếu có gì đó không hoạt động đúng, kiểm tra log của Lambda:

1. Vào **CloudWatch Console** → **Log groups**
2. Tìm `/aws/lambda/loginFunction` hoặc `/aws/lambda/getSongsFunction`
3. Mở log stream mới nhất để xem chi tiết lỗi
